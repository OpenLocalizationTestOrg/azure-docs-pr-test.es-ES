---
title: aaaAvailability y la escala en las plantillas de administrador de recursos de Azure | Documentos de Microsoft
description: "Tutorial de DotNet Core para máquinas virtuales de Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 494724b5-06af-4dea-a774-ba580cf27527
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a122d8e9536ea5fc2dc9c3f84042ed5c5179d783
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="f4007-103">Disponibilidad y escala en plantillas de Azure Resource Manager para máquinas virtuales Windows</span><span class="sxs-lookup"><span data-stu-id="f4007-103">Availability and scale in Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="f4007-104">Disponibilidad y escalabilidad consulte hello y toouptime demanda de toomeet de capacidad.</span><span class="sxs-lookup"><span data-stu-id="f4007-104">Availability and scale refer toouptime and hello ability toomeet demand.</span></span> <span data-ttu-id="f4007-105">Si una aplicación debe estar 99,9% de tiempo de hello, debe toohave una arquitectura que permite a varios recursos de proceso simultáneas.</span><span class="sxs-lookup"><span data-stu-id="f4007-105">If an application must be up 99.9% of hello time, it needs toohave an architecture that allows for multiple concurrent compute resources.</span></span> <span data-ttu-id="f4007-106">Por ejemplo, en lugar de tener un único sitio Web, una configuración con un mayor nivel de disponibilidad incluye varias instancias de hello al mismo sitio, con tecnología frente a ellos de equilibrio.</span><span class="sxs-lookup"><span data-stu-id="f4007-106">For instance, rather than having a single website, a configuration with a higher level of availability includes multiple instances of hello same site, with balancing technology in front of them.</span></span> <span data-ttu-id="f4007-107">En esta configuración, una instancia de la aplicación hello puede desactivarse por razones de mantenimiento, mientras que Hola restantes continúa toofunction.</span><span class="sxs-lookup"><span data-stu-id="f4007-107">In this configuration, one instance of hello application can be taken down for maintenance, while hello remaining continue toofunction.</span></span> <span data-ttu-id="f4007-108">Escala en hello otra parte hace referencia la petición de tooserve de capacidad de las aplicaciones de tooan.</span><span class="sxs-lookup"><span data-stu-id="f4007-108">Scale on hello other hand refers tooan applications ability tooserve demand.</span></span> <span data-ttu-id="f4007-109">Con una carga equilibrada aplicación, agregar o quitar instancias de grupo de hello permite una petición de toomeet tooscale de aplicación.</span><span class="sxs-lookup"><span data-stu-id="f4007-109">With a load balanced application, adding or removing instances from hello pool allows an application tooscale toomeet demand.</span></span>

<span data-ttu-id="f4007-110">Este documento describe cómo configurar el Hola implementación de ejemplo de tienda de música de disponibilidad y escalabilidad.</span><span class="sxs-lookup"><span data-stu-id="f4007-110">This document details how hello Music Store sample deployment is configured for availability and scale.</span></span> <span data-ttu-id="f4007-111">Se resaltan todas las dependencias y configuraciones únicas.</span><span class="sxs-lookup"><span data-stu-id="f4007-111">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="f4007-112">Para la mejor experiencia de hello, implementar previamente una instancia de hello solución tooyour suscripción de Azure y trabajar junto con la plantilla de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f4007-112">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="f4007-113">plantilla de Hello completa puede encontrarse aquí: [implementación de la tienda de música en Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="f4007-113">hello complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="availability-set"></a><span data-ttu-id="f4007-114">Conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="f4007-114">Availability Set</span></span>
<span data-ttu-id="f4007-115">Un conjunto de disponibilidad abarca de forma lógica máquinas virtuales de Azure entre hosts físicos y otros componentes de infraestructura tales como fuentes de alimentación y hardware de red físico.</span><span class="sxs-lookup"><span data-stu-id="f4007-115">An Availability Set logically spans Azure Virtual Machines across physical hosts and other infrastructural components such as power supplies and physical networking hardware.</span></span> <span data-ttu-id="f4007-116">Los conjuntos de disponibilidad garantizan que no todas las máquinas virtuales se vean afectadas durante las tareas de mantenimiento, los errores de dispositivo u otros tiempos de inactividad.</span><span class="sxs-lookup"><span data-stu-id="f4007-116">Availability sets ensure that during maintenance, device failure, or other down time, not all virtual machines are effected.</span></span> <span data-ttu-id="f4007-117">Un conjunto de disponibilidad se pueden agregar plantilla de Azure Resource Manager tooan usando Visual Studio agregar Asistente para nuevo recurso de Hola o insertar un valor JSON válido en una plantilla.</span><span class="sxs-lookup"><span data-stu-id="f4007-117">An Availability Set can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or inserting valid JSON into a template.</span></span>

<span data-ttu-id="f4007-118">Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [conjunto de disponibilidad](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L368).</span><span class="sxs-lookup"><span data-stu-id="f4007-118">Follow this link toosee hello JSON sample within hello Resource Manager template – [Availability Set](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L368).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "availability-set"
  },
  "properties": {
  }
}
```

<span data-ttu-id="f4007-119">Un conjunto de disponibilidad se declara como una propiedad de un recurso de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f4007-119">An Availability Set is declared as a property of a Virtual Machine resource.</span></span> 

<span data-ttu-id="f4007-120">Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [conjunto de disponibilidad de la asociación con la máquina Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L302).</span><span class="sxs-lookup"><span data-stu-id="f4007-120">Follow this link toosee hello JSON sample within hello Resource Manager template – [Availability Set association with Virtual Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L302).</span></span>

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
<span data-ttu-id="f4007-121">disponibilidad de Hello establecida tal como se muestra de Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f4007-121">hello availability set as seen from hello Azure portal.</span></span> <span data-ttu-id="f4007-122">Cada máquina virtual y los detalles sobre la configuración de Hola se detallan aquí.</span><span class="sxs-lookup"><span data-stu-id="f4007-122">Each virtual machine and details about hello configuration are detailed here.</span></span>

![Conjunto de disponibilidad](./media/dotnet-core-4-availability-scale/ase-win.png)

<span data-ttu-id="f4007-124">Para más información detallada sobre los conjuntos de disponibilidad, consulte [Administración de la disponibilidad de las máquinas virtuales](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f4007-124">For in-depth information on Availability Sets, see [Manage availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="network-load-balancer"></a><span data-ttu-id="f4007-125">Equilibrador de carga de red</span><span class="sxs-lookup"><span data-stu-id="f4007-125">Network Load Balancer</span></span>
<span data-ttu-id="f4007-126">Mientras que un conjunto de disponibilidad proporciona tolerancia a errores, un equilibrador de carga hace muchas instancias de aplicación hello estén disponibles en una única dirección de red.</span><span class="sxs-lookup"><span data-stu-id="f4007-126">Whereas an availability set provides application fault tolerance, a load balancer makes many instances of hello application available on a single network address.</span></span> <span data-ttu-id="f4007-127">Se pueden hospedar varias instancias de una aplicación en varias máquinas virtuales, cada uno conectado tooa equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="f4007-127">Multiple instances of an application can be hosted on many virtual machines, each one connected tooa load balancer.</span></span> <span data-ttu-id="f4007-128">Tal y como se tiene acceso a la aplicación hello, rutas de equilibrador de carga de Hola Hola solicitud entrante a través de los miembros de hello adjuntada.</span><span class="sxs-lookup"><span data-stu-id="f4007-128">As hello application is accessed, hello load balancer routes hello incoming request across hello attached members.</span></span> <span data-ttu-id="f4007-129">Un equilibrador de carga se pueden agregar utilizando Visual Studio agregar Asistente para nuevo recurso de Hola o insertando correctamente recursos JSON con formato en la plantilla de Azure Resource Manager Hola.</span><span class="sxs-lookup"><span data-stu-id="f4007-129">A Load Balancer can be added using hello Visual Studio Add New Resource Wizard, or by inserting properly formatted JSON resource into hello Azure Resource Manager template.</span></span>

<span data-ttu-id="f4007-130">Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [equilibrador de carga de red](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L198).</span><span class="sxs-lookup"><span data-stu-id="f4007-130">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L198).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer"
  },
  ........<truncated>
}
```

<span data-ttu-id="f4007-131">Dado que es de aplicación de ejemplo de Hola toohello expuesto internet con una dirección IP pública, esta dirección está asociada con el equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4007-131">Because hello sample application is exposed toohello internet with a public IP address, this address is associated with hello load balancer.</span></span> 

<span data-ttu-id="f4007-132">Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [asociaciones de equilibrador de carga de red con dirección IP pública](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span><span class="sxs-lookup"><span data-stu-id="f4007-132">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Load Balancer association with Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span></span>

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIpAddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

<span data-ttu-id="f4007-133">Desde Hola portal de Azure, hello información general del equilibrador de carga de red muestra asociación Hola con la dirección IP pública Hola.</span><span class="sxs-lookup"><span data-stu-id="f4007-133">From hello Azure portal, hello network load balancer overview shows hello association with hello public IP address.</span></span>

![Equilibrador de carga de red](./media/dotnet-core-4-availability-scale/nlb-win.png)

## <a name="load-balancer-rule"></a><span data-ttu-id="f4007-135">Regla de equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="f4007-135">Load Balancer Rule</span></span>
<span data-ttu-id="f4007-136">Cuando se utiliza un equilibrador de carga, se configuran reglas que controlan cómo se equilibra el tráfico a través de recursos de hello diseñado.</span><span class="sxs-lookup"><span data-stu-id="f4007-136">When using a load balancer, rules are configured that control how traffic is balanced across hello intended resources.</span></span> <span data-ttu-id="f4007-137">Con la aplicación de tienda de música de ejemplo de Hola, tráfico llega en el puerto 80 de la dirección IP pública hello y se distribuye a través del puerto 80 de todas las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f4007-137">With hello sample Music Store application, traffic arrives on port 80 of hello public IP address and is distributed across port 80 of all virtual machines.</span></span> 

<span data-ttu-id="f4007-138">Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [regla del equilibrador de carga](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L226).</span><span class="sxs-lookup"><span data-stu-id="f4007-138">Follow this link toosee hello JSON sample within hello Resource Manager template – [Load Balancer Rule](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L226).</span></span>

```json
"loadBalancingRules": [
  {
    "name": "[variables('loadBalencerRule')]",
    "properties": {
      "frontendIPConfiguration": {
        "id": "[concat(resourceId('Microsoft.Network/loadBalancers', variables('loadBalancerName')), '/frontendIPConfigurations/LoadBalancerFrontend')]"
      },
      "backendAddressPool": {
        "id": "[variables('lbPoolID')]"
      },
      "protocol": "Tcp",
      "frontendPort": 80,
      "backendPort": 80,
      "enableFloatingIP": false,
      "idleTimeoutInMinutes": 5,
      "probe": {
        "id": "[variables('lbProbeID')]"
      }
    }
  }
]
```

<span data-ttu-id="f4007-139">Una vista de red de hello cargar regla del equilibrador de desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4007-139">A view of hello network load balancer rule from hello portal.</span></span>

![Regla de equilibrador de carga de red](./media/dotnet-core-4-availability-scale/lbrule-win.png)

## <a name="load-balancer-probe"></a><span data-ttu-id="f4007-141">Sondeo de equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="f4007-141">Load Balancer Probe</span></span>
<span data-ttu-id="f4007-142">equilibrador de carga de Hello también necesita toomonitor cada máquina virtual para que se atienden las solicitudes solo toorunning sistemas.</span><span class="sxs-lookup"><span data-stu-id="f4007-142">hello load balancer also needs toomonitor each virtual machine so that requests are served only toorunning systems.</span></span> <span data-ttu-id="f4007-143">Esta supervisión se realiza mediante un sondeo constante en un puerto definido previamente.</span><span class="sxs-lookup"><span data-stu-id="f4007-143">This monitoring takes place by constant probing of a pre-defined port.</span></span> <span data-ttu-id="f4007-144">implementación de la tienda de música de Hello es máquinas virtuales de tooprobe configurado el puerto 80 en todos los incluye.</span><span class="sxs-lookup"><span data-stu-id="f4007-144">hello Music Store deployment is configured tooprobe port 80 on all included virtual machines.</span></span> 

<span data-ttu-id="f4007-145">Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [sondeo del equilibrador de carga](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L247).</span><span class="sxs-lookup"><span data-stu-id="f4007-145">Follow this link toosee hello JSON sample within hello Resource Manager template – [Load Balancer Probe](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L247).</span></span>

```json
"probes": [
  {
    "properties": {
      "protocol": "Tcp",
      "port": 80,
      "intervalInSeconds": 15,
      "numberOfProbes": 2
    },
    "name": "lbprobe"
  }
]
```

<span data-ttu-id="f4007-146">sondeo de equilibrador de carga de Hello ven de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f4007-146">hello load balancer probe seen from hello Azure portal.</span></span>

![Sondeo de equilibrador de carga de red](./media/dotnet-core-4-availability-scale/lbprobe-win.png)

## <a name="inbound-nat-rules"></a><span data-ttu-id="f4007-148">Reglas NAT de entrada</span><span class="sxs-lookup"><span data-stu-id="f4007-148">Inbound NAT Rules</span></span>
<span data-ttu-id="f4007-149">Cuando se utiliza un equilibrador de carga, las reglas deben toobe implanten que proporcionan acceso con equilibrio de carga no tooeach Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="f4007-149">When using a Load Balancer, rules need toobe put into place that provide non-load balanced access tooeach Virtual Machine.</span></span> <span data-ttu-id="f4007-150">Por ejemplo, al crear una conexión RDP con cada máquina virtual, este tráfico no debe tener equilibrio de carga; en su lugar, se debe configurar una ruta de acceso predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f4007-150">For instance, when creating an RDP connection with each virtual machine, this traffic should not be load balanced, rather a pre-determined path should be configured.</span></span> <span data-ttu-id="f4007-151">Las rutas de acceso predeterminadas se configuran mediante un recurso de regla NAT de entrada.</span><span class="sxs-lookup"><span data-stu-id="f4007-151">Pre-determined paths are configured using an Inbound NAT Rule resource.</span></span> <span data-ttu-id="f4007-152">Con este recurso, la comunicación entrante puede ser asignado tooindividual máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f4007-152">Using this resource, inbound communication can be mapped tooindividual Virtual Machines.</span></span> 

<span data-ttu-id="f4007-153">Con la aplicación de la tienda de música de hello, un puerto a partir de 5000 es asignada tooport 3389 en cada máquina Virtual para el acceso RDP.</span><span class="sxs-lookup"><span data-stu-id="f4007-153">With hello Music Store application, a port starting at 5000 is mapped tooport 3389 on each Virtual Machine for RDP access.</span></span> <span data-ttu-id="f4007-154">Hola `copyindex()` función es tooincrement usado Hola puerto de entrada, que Hola segunda Máquina Virtual recibe un puerto de entrada de 5001, Hola 5002 tercera y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="f4007-154">hello `copyindex()` function is used tooincrement hello incoming port, such that hello second Virtual Machine receives an incoming port of 5001, hello third 5002, and so on.</span></span>

<span data-ttu-id="f4007-155">Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [reglas de NAT de entrada](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L260).</span><span class="sxs-lookup"><span data-stu-id="f4007-155">Follow this link toosee hello JSON sample within hello Resource Manager template – [Inbound NAT Rules](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L260).</span></span> 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'RDP-VM', copyIndex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
  "copy": {
    "name": "lbNatLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
  ],
  "properties": {
    "frontendIPConfiguration": {
      "id": "[variables('ipConfigID')]"
    },
    "protocol": "tcp",
    "frontendPort": "[copyIndex(5000)]",
    "backendPort": 3389,
    "enableFloatingIP": false
  }
}
```

<span data-ttu-id="f4007-156">Ejemplo de una regla NAT de entrada como Hola encontrada en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f4007-156">One example inbound NAT rule as seen in hello Azure portal.</span></span> <span data-ttu-id="f4007-157">Se crea una regla de NAT de RDP para cada máquina virtual en la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4007-157">An RDP NAT rule is created for each virtual machine in hello deployment.</span></span>

![Regla NAT de entrada](./media/dotnet-core-4-availability-scale/natrule-win.png)

<span data-ttu-id="f4007-159">Para obtener información detallada sobre Hola equilibrador de carga de red de Azure, vea [equilibrio de carga para servicios de infraestructura de Azure](load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f4007-159">For in-depth information on hello Azure Network Load Balancer, see [Load balancing for Azure infrastructure services](load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="deploy-multiple-vms"></a><span data-ttu-id="f4007-160">Implementación de varias máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="f4007-160">Deploy multiple VMs</span></span>
<span data-ttu-id="f4007-161">Por último, para una función de tooeffectively conjunto de disponibilidad o equilibrio de carga, son necesarias varias máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f4007-161">Finally, for an Availability Set or Load Balancer tooeffectively function, multiple virtual machines are required.</span></span> <span data-ttu-id="f4007-162">Varias máquinas virtuales pueden implementarse mediante la función de copia de plantilla de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f4007-162">Multiple VMs can be deployed using hello Azure Resource Manager template copy function.</span></span> <span data-ttu-id="f4007-163">Mediante la función de copia de hello, no es necesario toodefine un número finito de máquinas virtuales, en su lugar este valor se puede proporcionar dinámicamente en tiempo de Hola de implementación.</span><span class="sxs-lookup"><span data-stu-id="f4007-163">Using hello copy function, it is not necessary toodefine a finite number of Virtual Machines, rather this value can be dynamically provided at hello time of deployment.</span></span> <span data-ttu-id="f4007-164">función de copia de Hello consume número Hola de toobe instancias creado e identificadores de implementar el número apropiado de Hola de máquinas virtuales y recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="f4007-164">hello copy function consumes hello number of instances toobe created and handles deploying hello proper number of virtual machines and associated resources.</span></span>

<span data-ttu-id="f4007-165">En la plantilla de ejemplo de la tienda de música de hello, se define un parámetro que toma un número de instancia.</span><span class="sxs-lookup"><span data-stu-id="f4007-165">In hello Music Store Sample template, a parameter is defined that takes in an instance count.</span></span> <span data-ttu-id="f4007-166">Este número se utiliza a lo largo de la plantilla de hello al crear máquinas virtuales y recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="f4007-166">This number is used throughout hello template when creating virtual machines and related resources.</span></span>

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 2,
  "metadata": {
    "description": "Number of VM instances toobe created behind load balancer."
  }
},
```

<span data-ttu-id="f4007-167">En hello recurso de máquina Virtual, bucles de copia de Hola se da un nombre y Hola número de instancias parámetro usa toocontrol Hola un número de copias resultantes.</span><span class="sxs-lookup"><span data-stu-id="f4007-167">On hello Virtual Machine resource, hello copy loop is given a name and hello number of instances parameter used toocontrol hello number of resulting copies.</span></span>

<span data-ttu-id="f4007-168">Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [función de copia de la máquina Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L290).</span><span class="sxs-lookup"><span data-stu-id="f4007-168">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine Copy Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L290).</span></span> 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  }
```

<span data-ttu-id="f4007-169">iteración actual de Hola de función de copia de hello puede obtenerse con hello `copyIndex()` función.</span><span class="sxs-lookup"><span data-stu-id="f4007-169">hello current iteration of hello copy function can be accessed with hello `copyIndex()` function.</span></span> <span data-ttu-id="f4007-170">valor de Hola de función de índice de hello copia puede ser usado tooname las máquinas virtuales y otros recursos.</span><span class="sxs-lookup"><span data-stu-id="f4007-170">hello value of hello copy index function can be used tooname virtual machines and other resources.</span></span> <span data-ttu-id="f4007-171">Por ejemplo, si se implementan dos instancias de una máquina virtual, necesitan nombres diferentes.</span><span class="sxs-lookup"><span data-stu-id="f4007-171">For instance, if two instances of a virtual machine are deployed, they need different names.</span></span> <span data-ttu-id="f4007-172">Hola `copyIndex()` función puede utilizarse como parte de la máquina virtual de hello nombre toocreate un nombre único.</span><span class="sxs-lookup"><span data-stu-id="f4007-172">hello `copyIndex()` function can be used as part of hello virtual machine name toocreate a unique name.</span></span> <span data-ttu-id="f4007-173">Un ejemplo de Hola `copyindex()` función que se usa para asignar nombres a fines puede verse en hello recurso de máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="f4007-173">An example of hello `copyindex()` function used for naming purposes can be seen in hello Virtual Machine resource.</span></span> <span data-ttu-id="f4007-174">En este caso, el nombre del equipo de hello es una concatenación de hello `vmName` hello y parámetro `copyIndex()` función.</span><span class="sxs-lookup"><span data-stu-id="f4007-174">Here, hello computer name is a concatenation of hello `vmName` parameter, and hello `copyIndex()` function.</span></span> 

<span data-ttu-id="f4007-175">Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [función de copia del índice](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L309).</span><span class="sxs-lookup"><span data-stu-id="f4007-175">Follow this link toosee hello JSON sample within hello Resource Manager template – [Copy Index Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L309).</span></span> 

```json
"osProfile": {
  "computerName": "[concat(variables('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "adminPassword": "[parameters('adminPassword')]"
}
```

<span data-ttu-id="f4007-176">Hola `copyIndex` función se utiliza varias veces en la plantilla de ejemplo de Hola tienda de música.</span><span class="sxs-lookup"><span data-stu-id="f4007-176">hello `copyIndex` function is used several times in hello Music Store sample template.</span></span> <span data-ttu-id="f4007-177">Recursos y utilización de las funciones `copyIndex` incluyen tooa nada específico única instancia Hola máquina virtual de este tipo e interfaz de red, las reglas del equilibrador de carga, y cualquier depende de las funciones.</span><span class="sxs-lookup"><span data-stu-id="f4007-177">Resources and functions utilizing `copyIndex` include anything specific tooa single instance of hello virtual machine such and network interface, load balancer rules, and any depends on functions.</span></span> 

<span data-ttu-id="f4007-178">Para obtener más información sobre la función de copia de hello, consulte [crear varias instancias de recursos en el Administrador de recursos de Azure](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="f4007-178">For more information on hello copy function, see [Create multiple instances of resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="f4007-179">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="f4007-179">Next step</span></span>
<hr>

[<span data-ttu-id="f4007-180">Paso 4: implementación de aplicaciones con plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f4007-180">Step 4 - Application Deployment with Azure Resource Manager Templates</span></span>](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

