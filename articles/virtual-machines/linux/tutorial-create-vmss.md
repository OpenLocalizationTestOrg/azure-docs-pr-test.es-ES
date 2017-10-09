---
title: "aaaCreate conjuntos de escalas de máquina Virtual para Linux en Azure | Documentos de Microsoft"
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
ms.openlocfilehash: 00dd81043f9be46ef2dc6dfe97eefdb20944ee13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a><span data-ttu-id="cd0ce-103">Creación de un conjunto de escalado de máquinas virtuales e implementación de una aplicación de alta disponibilidad en Linux</span><span class="sxs-lookup"><span data-stu-id="cd0ce-103">Create a Virtual Machine Scale Set and deploy a highly available app on Linux</span></span>
<span data-ttu-id="cd0ce-104">Un conjunto de escalas de máquina virtual permite toodeploy y administrar un conjunto de máquinas virtuales idénticos, la escala automática.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-104">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="cd0ce-105">Puede escalar el número de Hola de máquinas virtuales en el conjunto de escalas de hello manualmente, o definir tooautoscale reglas en función de uso de CPU, la demanda de memoria o el tráfico de red.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-105">You can scale hello number of VMs in hello scale set manually, or define rules tooautoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="cd0ce-106">En este tutorial, implementará un conjunto de escalado de máquinas virtuales en Azure.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="cd0ce-107">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="cd0ce-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cd0ce-108">Usar en la nube init toocreate una tooscale de aplicación</span><span class="sxs-lookup"><span data-stu-id="cd0ce-108">Use cloud-init toocreate an app tooscale</span></span>
> * <span data-ttu-id="cd0ce-109">Crear un conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="cd0ce-109">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="cd0ce-110">Aumentar o disminuir el número de Hola de instancias de un conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="cd0ce-110">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="cd0ce-111">Ver la información de conexión de las instancias del conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="cd0ce-111">View connection info for scale set instances</span></span>
> * <span data-ttu-id="cd0ce-112">Usar discos de datos con conjuntos de escalado</span><span class="sxs-lookup"><span data-stu-id="cd0ce-112">Use data disks in a scale set</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="cd0ce-113">Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="cd0ce-114">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="cd0ce-115">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cd0ce-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="scale-set-overview"></a><span data-ttu-id="cd0ce-116">Introducción al conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="cd0ce-116">Scale Set overview</span></span>
<span data-ttu-id="cd0ce-117">Un conjunto de escalas de máquina virtual permite toodeploy y administrar un conjunto de máquinas virtuales idénticos, la escala automática.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-117">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="cd0ce-118">Escala establece uso Hola mismos componentes tal y como ha aprendido en el tutorial anterior Hola demasiado[crear máquinas virtuales de alta disponibilidad](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="cd0ce-118">Scale sets use hello same components as you learned about in hello previous tutorial too[Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="cd0ce-119">Las máquinas virtuales de un conjunto de escalado se crean en un conjunto de disponibilidad y se distribuyen entre los dominios de error lógico y de actualización.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-119">VMs in a scale set are created in an availability set and distributed across logic fault and update domains.</span></span>

<span data-ttu-id="cd0ce-120">Las máquinas virtuales se crean según sea necesario en un conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-120">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="cd0ce-121">Definir toocontrol de reglas de escalado automático cómo y cuándo se agregan o se quitan del conjunto de escalas de hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-121">You define autoscale rules toocontrol how and when VMs are added or removed from hello scale set.</span></span> <span data-ttu-id="cd0ce-122">Estas reglas se pueden desencadenar en función de métricas como la carga de la CPU, el uso de la memoria o el tráfico de red.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-122">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="cd0ce-123">Escala establece compatibilidad con seguridad too1, 000 máquinas virtuales cuando se usa una imagen de la plataforma Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-123">Scale sets support up too1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="cd0ce-124">Para las cargas de trabajo de producción, es recomendable demasiado[crear una imagen de máquina virtual personalizada](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="cd0ce-124">For production workloads, you may wish too[Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="cd0ce-125">Puede crear las máquinas virtuales de too100 en una escala establecida cuando se usa una imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-125">You can create up too100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-tooscale"></a><span data-ttu-id="cd0ce-126">Crear una aplicación tooscale</span><span class="sxs-lookup"><span data-stu-id="cd0ce-126">Create an app tooscale</span></span>
<span data-ttu-id="cd0ce-127">Para su uso en producción, es recomendable demasiado[crear una imagen de máquina virtual personalizada](tutorial-custom-images.md) que incluye la aplicación instalada y configurada.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-127">For production use, you may wish too[Create a custom VM image](tutorial-custom-images.md) that includes your application installed and configured.</span></span> <span data-ttu-id="cd0ce-128">Para este tutorial, permite personalizar Hola que máquinas virtuales de primera tooquickly arranque ver una escala establecido en acción.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-128">For this tutorial, lets customize hello VMs on first boot tooquickly see a scale set in action.</span></span>

<span data-ttu-id="cd0ce-129">En un tutorial anterior, ha aprendido [cómo toocustomize una máquina virtual de Linux en el primer arranque](tutorial-automate-vm-deployment.md) con init de la nube.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-129">In a previous tutorial, you learned [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md) with cloud-init.</span></span> <span data-ttu-id="cd0ce-130">Puede usar Hola mismo tooinstall de archivo de configuración de nube init NGINX y ejecutar una aplicación sencilla de Node.js de "Hello World".</span><span class="sxs-lookup"><span data-stu-id="cd0ce-130">You can use hello same cloud-init configuration file tooinstall NGINX and run a simple 'Hello World' Node.js app.</span></span> 

<span data-ttu-id="cd0ce-131">En el shell actual, cree un archivo denominado *init.txt nube* y pegar Hola siguiente configuración.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-131">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="cd0ce-132">Por ejemplo, crear archivo hello en hello Shell en la nube, no en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-132">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="cd0ce-133">Escriba `sensible-editor cloud-init.txt` toocreate Hola archivo y ver una lista de editores disponibles.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-133">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="cd0ce-134">Asegúrese de que ese archivo de nube-init todo Hola se copia correctamente, especialmente Hola primera línea:</span><span class="sxs-lookup"><span data-stu-id="cd0ce-134">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

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


## <a name="create-a-scale-set"></a><span data-ttu-id="cd0ce-135">Creación de un conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="cd0ce-135">Create a scale set</span></span>
<span data-ttu-id="cd0ce-136">Antes de poder crear un conjunto de escalado, cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="cd0ce-136">Before you can create a scale set, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="cd0ce-137">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroupScaleSet* en hello *eastus* ubicación:</span><span class="sxs-lookup"><span data-stu-id="cd0ce-137">hello following example creates a resource group named *myResourceGroupScaleSet* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

<span data-ttu-id="cd0ce-138">Ahora, cree un conjunto de escalado de máquinas virtuales con [az vmss create](/cli/azure/vmss#create).</span><span class="sxs-lookup"><span data-stu-id="cd0ce-138">Now create a virtual machine scale set with [az vmss create](/cli/azure/vmss#create).</span></span> <span data-ttu-id="cd0ce-139">Hello en el ejemplo siguiente se crea un conjunto con nombre de escalas *myScaleSet*, utiliza Hola de toocustomize de archivo VM de hello init de la nube y genera claves SSH si no existen:</span><span class="sxs-lookup"><span data-stu-id="cd0ce-139">hello following example creates a scale set named *myScaleSet*, uses hello cloud-init file toocustomize hello VM, and generates SSH keys if they do not exist:</span></span>

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

<span data-ttu-id="cd0ce-140">Toma toocreate unos minutos y configurará todos los recursos de conjunto de escala de Hola y máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-140">It takes a few minutes toocreate and configure all hello scale set resources and VMs.</span></span> <span data-ttu-id="cd0ce-141">Hay tareas en segundo plano que continúan toorun después de hello CLI de Azure devuelve toohello símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-141">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="cd0ce-142">Es posible que otro par de minutos antes de que se puede tener acceso a la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-142">It may be another couple of minutes before you can access hello app.</span></span>


## <a name="allow-web-traffic"></a><span data-ttu-id="cd0ce-143">Permitir tráfico web</span><span class="sxs-lookup"><span data-stu-id="cd0ce-143">Allow web traffic</span></span>
<span data-ttu-id="cd0ce-144">Un equilibrador de carga se creó automáticamente como parte del conjunto de escalas de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-144">A load balancer was created automatically as part of hello virtual machine scale set.</span></span> <span data-ttu-id="cd0ce-145">equilibrador de carga de Hello distribuye el tráfico a través de un conjunto de máquinas virtuales definidas mediante reglas de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-145">hello load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="cd0ce-146">Puede aprender más sobre conceptos de equilibrador de carga y la configuración en el siguiente tutorial Hola, [cómo tooload equilibrar las máquinas virtuales en Azure](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="cd0ce-146">You can learn more about load balancer concepts and configuration in hello next tutorial, [How tooload balance virtual machines in Azure](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="cd0ce-147">tooallow tráfico tooreach hello web app, cree una regla con [crear regla de carga equilibrada de red az](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="cd0ce-147">tooallow traffic tooreach hello web app, create a rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="cd0ce-148">Hello en el ejemplo siguiente se crea una regla denominada *myLoadBalancerRuleWeb*:</span><span class="sxs-lookup"><span data-stu-id="cd0ce-148">hello following example creates a rule named *myLoadBalancerRuleWeb*:</span></span>

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

## <a name="test-your-app"></a><span data-ttu-id="cd0ce-149">Prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="cd0ce-149">Test your app</span></span>
<span data-ttu-id="cd0ce-150">toosee la aplicación Node.js en web de hello, obtener la dirección IP pública de Hola de un equilibrador de carga con [show de public-ip de red az](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="cd0ce-150">toosee your Node.js app on hello web, obtain hello public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="cd0ce-151">Hello en el ejemplo siguiente se obtiene la dirección IP de Hola para *myScaleSetLBPublicIP* creado como parte del conjunto de escalas de hello:</span><span class="sxs-lookup"><span data-stu-id="cd0ce-151">hello following example obtains hello IP address for *myScaleSetLBPublicIP* created as part of hello scale set:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="cd0ce-152">Escriba la dirección IP pública hello en el Explorador de web tooa.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-152">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="cd0ce-153">se muestra la aplicación Hello, incluido Hola nombre de host de hello VM ese Hola la carga del tráfico de equilibrador distribuida para:</span><span class="sxs-lookup"><span data-stu-id="cd0ce-153">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic to:</span></span>

![Ejecución de la aplicación Node.js](./media/tutorial-create-vmss/running-nodejs-app.png)

<span data-ttu-id="cd0ce-155">escala de hello toosee establecida en acción, se puede forzar actualización su carga de hello web explorador toosee equilibrador de distribuir el tráfico entre todas las máquinas virtuales de hello ejecutando la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-155">toosee hello scale set in action, you can force-refresh your web browser toosee hello load balancer distribute traffic across all hello VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="cd0ce-156">Tareas de administración</span><span class="sxs-lookup"><span data-stu-id="cd0ce-156">Management tasks</span></span>
<span data-ttu-id="cd0ce-157">A lo largo del ciclo de vida de Hola de conjunto de escalas de hello, puede que necesite toorun una o más tareas de administración.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-157">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="cd0ce-158">Además, puede que desee toocreate scripts que automaticen diversas tareas de ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-158">Additionally, you may want toocreate scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="cd0ce-159">Hola 2.0 de CLI de Azure proporciona una forma rápida toodo esas tareas.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-159">hello Azure CLI 2.0 provides a quick way toodo those tasks.</span></span> <span data-ttu-id="cd0ce-160">A continuación, presentamos algunas tareas comunes.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-160">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="cd0ce-161">Visualización de máquinas virtuales en un conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="cd0ce-161">View VMs in a scale set</span></span>
<span data-ttu-id="cd0ce-162">tooview una lista de máquinas virtuales en ejecución en la escala de conjunto, utilice [instancias de lista az vmss](/cli/azure/vmss#list-instances) como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="cd0ce-162">tooview a list of VMs running in your scale set, use [az vmss list-instances](/cli/azure/vmss#list-instances) as follows:</span></span>

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

<span data-ttu-id="cd0ce-163">Hola de salida es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cd0ce-163">hello output is similar toohello following example:</span></span>

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="cd0ce-164">Aumento o disminución de instancias de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="cd0ce-164">Increase or decrease VM instances</span></span>
<span data-ttu-id="cd0ce-165">número de hello toosee de instancias actualmente en una escala estableciste, use [presentación con az vmss](/cli/azure/vmss#show) y realizar consultas sobre *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="cd0ce-165">toosee hello number of instances you currently have in a scale set, use [az vmss show](/cli/azure/vmss#show) and query on *sku.capacity*:</span></span>

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

<span data-ttu-id="cd0ce-166">Puede, a continuación, manualmente aumentar o reducir el número de Hola de máquinas virtuales en la escala de hello establecida con [escala de vmss az](/cli/azure/vmss#scale).</span><span class="sxs-lookup"><span data-stu-id="cd0ce-166">You can then manually increase or decrease hello number of virtual machines in hello scale set with [az vmss scale](/cli/azure/vmss#scale).</span></span> <span data-ttu-id="cd0ce-167">Hello en el ejemplo siguiente se establece Hola número de máquinas virtuales de la escala establecida demasiado*5*:</span><span class="sxs-lookup"><span data-stu-id="cd0ce-167">hello following example sets hello number of VMs in your scale set too*5*:</span></span>

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

<span data-ttu-id="cd0ce-168">Las reglas de escalado automático le permiten definir cómo tooscale hacia arriba o hacia abajo el número de Hola de máquinas virtuales en la escala se establece en toodemand de respuesta como el tráfico de red o el uso de CPU.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-168">Autoscale rules let you define how tooscale up or down hello number of VMs in your scale set in response toodemand such as network traffic or CPU usage.</span></span> <span data-ttu-id="cd0ce-169">Actualmente, no se pueden establecer estas reglas en la CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-169">Currently, these rules cannot be set in Azure CLI 2.0.</span></span> <span data-ttu-id="cd0ce-170">Hola de uso [portal de Azure](https://portal.azure.com) tooconfigure Autoescala.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-170">Use hello [Azure portal](https://portal.azure.com) tooconfigure autoscale.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="cd0ce-171">Obtención de información de conexión</span><span class="sxs-lookup"><span data-stu-id="cd0ce-171">Get connection info</span></span>
<span data-ttu-id="cd0ce-172">información de conexión de tooobtain aproximadamente Hola a las máquinas virtuales en los conjuntos de escala, use [vmss az-instancia de lista-info conexión](/cli/azure/vmss#list-instance-connection-info).</span><span class="sxs-lookup"><span data-stu-id="cd0ce-172">tooobtain connection information about hello VMs in your scale sets, use [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info).</span></span> <span data-ttu-id="cd0ce-173">Este comando da como resultado la dirección IP pública Hola y el puerto para cada máquina virtual que permite tooconnect mediante SSH:</span><span class="sxs-lookup"><span data-stu-id="cd0ce-173">This command outputs hello public IP address and port for each VM that allows you tooconnect with SSH:</span></span>

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a><span data-ttu-id="cd0ce-174">Uso de discos de datos con conjuntos de escalado</span><span class="sxs-lookup"><span data-stu-id="cd0ce-174">Use data disks with scale sets</span></span>
<span data-ttu-id="cd0ce-175">Puede crear y usar discos de datos con conjuntos de escalado.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-175">You can create and use data disks with scale sets.</span></span> <span data-ttu-id="cd0ce-176">En un tutorial anterior, ha aprendido cómo demasiado[discos Azure administrar](tutorial-manage-disks.md) que contornos Hola prácticas recomendadas y mejoras de rendimiento para la creación de aplicaciones en los discos de datos en lugar de en disco de SO Hola.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-176">In a previous tutorial, you learned how too[Manage Azure disks](tutorial-manage-disks.md) that outlines hello best practices and performance improvements for building apps on data disks rather than hello OS disk.</span></span>

### <a name="create-scale-set-with-data-disks"></a><span data-ttu-id="cd0ce-177">Creación de conjunto de escalado con discos de datos</span><span class="sxs-lookup"><span data-stu-id="cd0ce-177">Create scale set with data disks</span></span>
<span data-ttu-id="cd0ce-178">toocreate una escala establecido y conectar discos de datos, agregar hello `--data-disk-sizes-gb` parámetro toohello [crear az vmss](/cli/azure/vmss#create) comando.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-178">toocreate a scale set and attach data disks, add hello `--data-disk-sizes-gb` parameter toohello [az vmss create](/cli/azure/vmss#create) command.</span></span> <span data-ttu-id="cd0ce-179">Hello en el ejemplo siguiente se crea una escala establecida con *50*Gb discos de datos adjunta la instancia de tooeach:</span><span class="sxs-lookup"><span data-stu-id="cd0ce-179">hello following example creates a scale set with *50*Gb data disks attached tooeach instance:</span></span>

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

<span data-ttu-id="cd0ce-180">Cuando se quitan las instancias de un conjunto de escalado, también se quitan los discos de datos conectados.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-180">When instances are removed from a scale set, any attached data disks are also removed.</span></span>

### <a name="add-data-disks"></a><span data-ttu-id="cd0ce-181">Adición de discos de datos</span><span class="sxs-lookup"><span data-stu-id="cd0ce-181">Add data disks</span></span>
<span data-ttu-id="cd0ce-182">establecer un tooinstances de disco de datos en la escala de tooadd, use [adjuntar disco de az vmss](/cli/azure/vmss/disk#attach).</span><span class="sxs-lookup"><span data-stu-id="cd0ce-182">tooadd a data disk tooinstances in your scale set, use [az vmss disk attach](/cli/azure/vmss/disk#attach).</span></span> <span data-ttu-id="cd0ce-183">Hello ejemplo siguiente se agrega un *50*instancia de tooeach de disco Gb:</span><span class="sxs-lookup"><span data-stu-id="cd0ce-183">hello following example adds a *50*Gb disk tooeach instance:</span></span>

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a><span data-ttu-id="cd0ce-184">Desacoplamiento de discos de datos</span><span class="sxs-lookup"><span data-stu-id="cd0ce-184">Detach data disks</span></span>
<span data-ttu-id="cd0ce-185">establecer un tooinstances de disco de datos en la escala de tooremove, use [desasociar el disco de vmss az](/cli/azure/vmss/disk#detach).</span><span class="sxs-lookup"><span data-stu-id="cd0ce-185">tooremove a data disk tooinstances in your scale set, use [az vmss disk detach](/cli/azure/vmss/disk#detach).</span></span> <span data-ttu-id="cd0ce-186">Hello en el ejemplo siguiente se quita disco de datos de hello en el LUN *2* de cada instancia de:</span><span class="sxs-lookup"><span data-stu-id="cd0ce-186">hello following example removes hello data disk at LUN *2* from each instance:</span></span>

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a><span data-ttu-id="cd0ce-187">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cd0ce-187">Next steps</span></span>
<span data-ttu-id="cd0ce-188">En este tutorial, ha creado un conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-188">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="cd0ce-189">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="cd0ce-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cd0ce-190">Usar en la nube init toocreate una tooscale de aplicación</span><span class="sxs-lookup"><span data-stu-id="cd0ce-190">Use cloud-init toocreate an app tooscale</span></span>
> * <span data-ttu-id="cd0ce-191">Crear un conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="cd0ce-191">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="cd0ce-192">Aumentar o disminuir el número de Hola de instancias de un conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="cd0ce-192">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="cd0ce-193">Ver la información de conexión de las instancias del conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="cd0ce-193">View connection info for scale set instances</span></span>
> * <span data-ttu-id="cd0ce-194">Usar discos de datos con conjuntos de escalado</span><span class="sxs-lookup"><span data-stu-id="cd0ce-194">Use data disks in a scale set</span></span>

<span data-ttu-id="cd0ce-195">Avanzar toohello siguiente tutorial toolearn más información sobre los conceptos de máquinas virtuales de equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="cd0ce-195">Advance toohello next tutorial toolearn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="cd0ce-196">[Load balance virtual machines](tutorial-load-balancer.md) (Equilibrio de carga de máquinas virtuales)</span><span class="sxs-lookup"><span data-stu-id="cd0ce-196">[Load balance virtual machines](tutorial-load-balancer.md)</span></span>