---
title: "plantillas de conjunto de aaaLearn acerca de la escala de máquinas virtuales | Documentos de Microsoft"
description: "Obtenga información acerca de toocreate una escala mínima viable establece plantilla para conjuntos de escalas de máquina virtual"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: b7a1cf6c03b22585e16db9c071d45795c8ae75df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a><span data-ttu-id="46543-103">Más información sobre las plantillas de conjuntos de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="46543-103">Learn about virtual machine scale set templates</span></span>
<span data-ttu-id="46543-104">[Plantillas de administrador de recursos de Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) es una excelente manera toodeploy grupos de recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="46543-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way toodeploy groups of related resources.</span></span> <span data-ttu-id="46543-105">Esta serie de tutoriales se muestra cómo toocreate una escala mínima viable establece plantilla y cómo toomodify esta toosuit plantilla diversos escenarios.</span><span class="sxs-lookup"><span data-stu-id="46543-105">This tutorial series shows how toocreate a minimum viable scale set template and how toomodify this template toosuit various scenarios.</span></span> <span data-ttu-id="46543-106">Todos los ejemplos proceden de este [repositorio de GitHub](https://github.com/gatneil/mvss).</span><span class="sxs-lookup"><span data-stu-id="46543-106">All examples come from this [GitHub repository](https://github.com/gatneil/mvss).</span></span> 

<span data-ttu-id="46543-107">Esta plantilla es previsto toobe simple.</span><span class="sxs-lookup"><span data-stu-id="46543-107">This template is intended toobe simple.</span></span> <span data-ttu-id="46543-108">Para obtener ejemplos más completos de escala definir plantillas, consulte hello [repositorio de GitHub de plantillas de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates) y busque las carpetas que contienen la cadena de hello `vmss`.</span><span class="sxs-lookup"><span data-stu-id="46543-108">For more complete examples of scale set templates, see hello [Azure Quickstart Templates GitHub repository](https://github.com/Azure/azure-quickstart-templates) and search for folders that contain hello string `vmss`.</span></span>

<span data-ttu-id="46543-109">Si ya está familiarizado con la creación de plantillas, puede omitir toohello toosee de sección "Pasos siguientes" ¿cómo toomodify esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="46543-109">If you are already familiar with creating templates, you can skip toohello "Next steps" section toosee how toomodify this template.</span></span>

## <a name="review-hello-template"></a><span data-ttu-id="46543-110">Plantilla de Hola de revisión</span><span class="sxs-lookup"><span data-stu-id="46543-110">Review hello template</span></span>

<span data-ttu-id="46543-111">Usar GitHub tooreview nuestra escala mínima viable establece plantilla, [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="46543-111">Use GitHub tooreview our minimum viable scale set template, [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span></span>

<span data-ttu-id="46543-112">En este tutorial, se examina Hola diff (`git diff master minimum-viable-scale-set`) toocreate Hola mínimo viable conjunto de escalado de plantilla parte por parte.</span><span class="sxs-lookup"><span data-stu-id="46543-112">In this tutorial, we examine hello diff (`git diff master minimum-viable-scale-set`) toocreate hello minimum viable scale set template piece by piece.</span></span>

## <a name="define-schema-and-contentversion"></a><span data-ttu-id="46543-113">Definición de $schema y contentVersion</span><span class="sxs-lookup"><span data-stu-id="46543-113">Define $schema and contentVersion</span></span>
<span data-ttu-id="46543-114">En primer lugar, definimos `$schema` y `contentVersion` en plantilla Hola.</span><span class="sxs-lookup"><span data-stu-id="46543-114">First, we define `$schema` and `contentVersion` in hello template.</span></span> <span data-ttu-id="46543-115">Hola `$schema` elemento define la versión de Hola de idioma de plantilla de Hola y se utiliza para el resaltado de sintaxis de Visual Studio y las características de validación similar.</span><span class="sxs-lookup"><span data-stu-id="46543-115">hello `$schema` element defines hello version of hello template language and is used for Visual Studio syntax highlighting and similar validation features.</span></span> <span data-ttu-id="46543-116">Hola `contentVersion` elemento no se usa en Azure.</span><span class="sxs-lookup"><span data-stu-id="46543-116">hello `contentVersion` element is not used by Azure.</span></span> <span data-ttu-id="46543-117">En su lugar, le ayuda a realizar un seguimiento de la versión de la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="46543-117">Instead, it helps you keep track of hello template version.</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a><span data-ttu-id="46543-118">Definición de parámetros</span><span class="sxs-lookup"><span data-stu-id="46543-118">Define parameters</span></span>
<span data-ttu-id="46543-119">Después, definimos dos parámetros, `adminUsername` y `adminPassword`.</span><span class="sxs-lookup"><span data-stu-id="46543-119">Next, we define two parameters, `adminUsername` and `adminPassword`.</span></span> <span data-ttu-id="46543-120">Los parámetros son valores que especifique en el momento de saludo de la implementación.</span><span class="sxs-lookup"><span data-stu-id="46543-120">Parameters are values you specify at hello time of deployment.</span></span> <span data-ttu-id="46543-121">Hola `adminUsername` parámetro es simplemente una `string` tipo, sino también porque `adminPassword` es un secreto, proporcionamos a tipo `securestring`.</span><span class="sxs-lookup"><span data-stu-id="46543-121">hello `adminUsername` parameter is simply a `string` type, but because `adminPassword` is a secret, we give it type `securestring`.</span></span> <span data-ttu-id="46543-122">Más adelante, estos parámetros se pasan a la configuración de conjunto de escalado de Hola.</span><span class="sxs-lookup"><span data-stu-id="46543-122">Later, these parameters are passed into hello scale set configuration.</span></span>

```json
  "parameters": {
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    }
  },
```
## <a name="define-variables"></a><span data-ttu-id="46543-123">Definición de variables</span><span class="sxs-lookup"><span data-stu-id="46543-123">Define variables</span></span>
<span data-ttu-id="46543-124">Plantillas de administrador de recursos también le permiten definir toobe de variables que se usará más adelante en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="46543-124">Resource Manager templates also let you define variables toobe used later in hello template.</span></span> <span data-ttu-id="46543-125">El ejemplo no utiliza las variables, por lo que hemos dejado objeto JSON de hello vacía.</span><span class="sxs-lookup"><span data-stu-id="46543-125">Our example doesn't use any variables, so we've left hello JSON object empty.</span></span>

```json
  "variables": {},
```

## <a name="define-resources"></a><span data-ttu-id="46543-126">Definición de recursos</span><span class="sxs-lookup"><span data-stu-id="46543-126">Define resources</span></span>
<span data-ttu-id="46543-127">A continuación figura la sección de recursos de Hola de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="46543-127">Next is hello resources section of hello template.</span></span> <span data-ttu-id="46543-128">Aquí, definir lo que realmente desea toodeploy.</span><span class="sxs-lookup"><span data-stu-id="46543-128">Here, you define what you actually want toodeploy.</span></span> <span data-ttu-id="46543-129">A diferencia de `parameters` y `variables` (que son objetos), `resources` es una lista JSON de objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="46543-129">Unlike `parameters` and `variables` (which are JSON objects), `resources` is a JSON list of JSON objects.</span></span>

```json
   "resources": [
```

<span data-ttu-id="46543-130">Todos los recursos requieren las propiedades `type`, `name`, `apiVersion` y `location`.</span><span class="sxs-lookup"><span data-stu-id="46543-130">All resources require `type`, `name`, `apiVersion`, and `location` properties.</span></span> <span data-ttu-id="46543-131">El primer recurso de este ejemplo tiene el tipo `Microsft.Network/virtualNetwork`, el nombre `myVnet` y el valor de apiVersion `2016-03-30`.</span><span class="sxs-lookup"><span data-stu-id="46543-131">This example's first resource has type `Microsft.Network/virtualNetwork`, name `myVnet`, and apiVersion `2016-03-30`.</span></span> <span data-ttu-id="46543-132">(versión API toofind hello más reciente para un tipo de recurso, vea hello [documentación de la API de REST de Azure](https://docs.microsoft.com/rest/api/).)</span><span class="sxs-lookup"><span data-stu-id="46543-132">(toofind hello latest API version for a resource type, see hello [Azure REST API documentation](https://docs.microsoft.com/rest/api/).)</span></span>

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a><span data-ttu-id="46543-133">Especificación de ubicación</span><span class="sxs-lookup"><span data-stu-id="46543-133">Specify location</span></span>
<span data-ttu-id="46543-134">ubicación de hello toospecify para la red virtual de hello, usamos un [función de plantilla de administrador de recursos](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="46543-134">toospecify hello location for hello virtual network, we use a [Resource Manager template function](../azure-resource-manager/resource-group-template-functions.md).</span></span> <span data-ttu-id="46543-135">Esta función debe estar entre comillas y corchetes de la siguiente manera: `"[<template-function>]"`.</span><span class="sxs-lookup"><span data-stu-id="46543-135">This function must be enclosed in quotes and square brackets like this: `"[<template-function>]"`.</span></span> <span data-ttu-id="46543-136">En este caso, usamos hello `resourceGroup` función.</span><span class="sxs-lookup"><span data-stu-id="46543-136">In this case, we use hello `resourceGroup` function.</span></span> <span data-ttu-id="46543-137">Toma ningún argumento y devuelve un objeto JSON con metadatos sobre esta implementación se está implementando en el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="46543-137">It takes in no arguments and returns a JSON object with metadata about hello resource group this deployment is being deployed to.</span></span> <span data-ttu-id="46543-138">grupo de recursos de Hola se establece por usuario de hello en tiempo de Hola de implementación.</span><span class="sxs-lookup"><span data-stu-id="46543-138">hello resource group is set by hello user at hello time of deployment.</span></span> <span data-ttu-id="46543-139">Después, se índice en este objeto JSON con `.location` ubicación de hello tooget desde un objeto JSON Hola.</span><span class="sxs-lookup"><span data-stu-id="46543-139">We then index into this JSON object with `.location` tooget hello location from hello JSON object.</span></span>

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a><span data-ttu-id="46543-140">Especificación de las propiedades de la red virtual</span><span class="sxs-lookup"><span data-stu-id="46543-140">Specify virtual network properties</span></span>
<span data-ttu-id="46543-141">Cada recurso de administrador de recursos tiene su propio `properties` sección de recursos de toohello específico de configuraciones.</span><span class="sxs-lookup"><span data-stu-id="46543-141">Each Resource Manager resource has its own `properties` section for configurations specific toohello resource.</span></span> <span data-ttu-id="46543-142">En este caso, especificamos red virtual Hola debe tener una subred con el intervalo de direcciones IP privadas de hello `10.0.0.0/16`.</span><span class="sxs-lookup"><span data-stu-id="46543-142">In this case, we specify that hello virtual network should have one subnet using hello private IP address range `10.0.0.0/16`.</span></span> <span data-ttu-id="46543-143">Un conjunto de escalado siempre está dentro de una subred,</span><span class="sxs-lookup"><span data-stu-id="46543-143">A scale set is always contained within one subnet.</span></span> <span data-ttu-id="46543-144">y no puede abarcar subredes.</span><span class="sxs-lookup"><span data-stu-id="46543-144">It cannot span subnets.</span></span>

```json
       "properties": {
         "addressSpace": {
           "addressPrefixes": [
             "10.0.0.0/16"
           ]
         },
         "subnets": [
           {
             "name": "mySubnet",
             "properties": {
               "addressPrefix": "10.0.0.0/16"
             }
           }
         ]
       }
     },
```

## <a name="add-dependson-list"></a><span data-ttu-id="46543-145">Incorporación de la lista dependsOn</span><span class="sxs-lookup"><span data-stu-id="46543-145">Add dependsOn list</span></span>
<span data-ttu-id="46543-146">Además requiere toohello `type`, `name`, `apiVersion`, y `location` propiedades, cada recurso pueden tener una función opcional `dependsOn` lista de cadenas.</span><span class="sxs-lookup"><span data-stu-id="46543-146">In addition toohello required `type`, `name`, `apiVersion`, and `location` properties, each resource can have an optional `dependsOn` list of strings.</span></span> <span data-ttu-id="46543-147">Esta lista especifica qué otros recursos de esta implementación deben finalizar antes de implementar este recurso.</span><span class="sxs-lookup"><span data-stu-id="46543-147">This list specifies which other resources from this deployment must finish before deploying this resource.</span></span>

<span data-ttu-id="46543-148">En este caso, hay solo un elemento de lista de hello, red virtual de hello del anterior ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="46543-148">In this case, there is only one element in hello list, hello virtual network from hello previous example.</span></span> <span data-ttu-id="46543-149">Especificamos esta dependencia porque escala Hola conjunto requiere Hola red tooexist antes de crear todas las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="46543-149">We specify this dependency because hello scale set needs hello network tooexist before creating any VMs.</span></span> <span data-ttu-id="46543-150">De esta manera, conjunto de escalas de hello puede dar a estas direcciones IP privadas de máquinas virtuales de intervalo de direcciones IP de hello especificado anteriormente hello en Propiedades de red.</span><span class="sxs-lookup"><span data-stu-id="46543-150">This way, hello scale set can give these VMs private IP addresses from hello IP address range previously specified in hello network properties.</span></span> <span data-ttu-id="46543-151">formato de Hola de cada cadena en la lista de dependsOn de hello es `<type>/<name>`.</span><span class="sxs-lookup"><span data-stu-id="46543-151">hello format of each string in hello dependsOn list is `<type>/<name>`.</span></span> <span data-ttu-id="46543-152">Use Hola mismo `type` y `name` usado previamente en la definición de recursos de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="46543-152">Use hello same `type` and `name` used previously in hello virtual network resource definition.</span></span>

```json
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "apiVersion": "2016-04-30-preview",
       "location": "[resourceGroup().location]",
       "dependsOn": [
         "Microsoft.Network/virtualNetworks/myVnet"
       ],
```
## <a name="specify-scale-set-properties"></a><span data-ttu-id="46543-153">Especificación de propiedades de conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="46543-153">Specify scale set properties</span></span>
<span data-ttu-id="46543-154">Conjuntos de escalas tienen muchas propiedades para personalizar las máquinas virtuales de hello en el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="46543-154">Scale sets have many properties for customizing hello VMs in hello scale set.</span></span> <span data-ttu-id="46543-155">Para obtener una lista completa de estas propiedades, vea hello [conjunto de escalado de documentación de la API de REST](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span><span class="sxs-lookup"><span data-stu-id="46543-155">For a full list of these properties, see hello [scale set REST API documentation](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span></span> <span data-ttu-id="46543-156">En ese tutorial solo establecemos algunas propiedades de uso frecuente.</span><span class="sxs-lookup"><span data-stu-id="46543-156">For this tutorial, we will set only a few commonly used properties.</span></span>
### <a name="supply-vm-size-and-capacity"></a><span data-ttu-id="46543-157">Suministro de capacidad y tamaño de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="46543-157">Supply VM size and capacity</span></span>
<span data-ttu-id="46543-158">escala de Hello establece necesidades tooknow qué tamaño de VM toocreate ("nombre de sku") y cuántos tal toocreate de máquinas virtuales ("capacidad de sku").</span><span class="sxs-lookup"><span data-stu-id="46543-158">hello scale set needs tooknow what size of VM toocreate ("sku name") and how many such VMs toocreate ("sku capacity").</span></span> <span data-ttu-id="46543-159">toosee los tamaños de VM están disponibles, vea hello [documentación de tamaños de máquina virtual](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span><span class="sxs-lookup"><span data-stu-id="46543-159">toosee which VM sizes are available, see hello [VM Sizes documentation](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span></span>

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a><span data-ttu-id="46543-160">Elección del tipo de actualizaciones</span><span class="sxs-lookup"><span data-stu-id="46543-160">Choose type of updates</span></span>
<span data-ttu-id="46543-161">conjunto de escalas de Hello también debe tooknow cómo toohandle se actualiza en el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="46543-161">hello scale set also needs tooknow how toohandle updates on hello scale set.</span></span> <span data-ttu-id="46543-162">En estos momentos hay dos opciones, `Manual` y `Automatic`.</span><span class="sxs-lookup"><span data-stu-id="46543-162">Currently, there are two options, `Manual` and `Automatic`.</span></span> <span data-ttu-id="46543-163">Para obtener más información sobre las diferencias de hello entre dos hello, consulte la documentación de hello en [cómo tooupgrade un conjunto de escalado de](./virtual-machine-scale-sets-upgrade-scale-set.md).</span><span class="sxs-lookup"><span data-stu-id="46543-163">For more information on hello differences between hello two, see hello documentation on [how tooupgrade a scale set](./virtual-machine-scale-sets-upgrade-scale-set.md).</span></span>

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a><span data-ttu-id="46543-164">Elección del sistema operativo de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="46543-164">Choose VM operating system</span></span>
<span data-ttu-id="46543-165">escala de Hello establece necesidades tooknow qué tooput de sistema operativo en máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="46543-165">hello scale set needs tooknow what operating system tooput on hello VMs.</span></span> <span data-ttu-id="46543-166">En este caso, creamos hello las máquinas virtuales con una imagen de 16.04 LTS Ubuntu totalmente revisada.</span><span class="sxs-lookup"><span data-stu-id="46543-166">Here, we create hello VMs with a fully patched Ubuntu 16.04-LTS image.</span></span>

```json
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
               "publisher": "Canonical",
               "offer": "UbuntuServer",
               "sku": "16.04-LTS",
               "version": "latest"
             }
           },
```

### <a name="specify-computernameprefix"></a><span data-ttu-id="46543-167">Especificación de computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="46543-167">Specify computerNamePrefix</span></span>
<span data-ttu-id="46543-168">conjunto de escalas de Hello implementa varias máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="46543-168">hello scale set deploys multiple VMs.</span></span> <span data-ttu-id="46543-169">En lugar de especificar el nombre de cada máquina virtual, especificamos `computerNamePrefix`.</span><span class="sxs-lookup"><span data-stu-id="46543-169">Instead of specifying each VM name, we specify `computerNamePrefix`.</span></span> <span data-ttu-id="46543-170">Hello conjunto de escalas de anexa un prefijo de toohello de índice para cada máquina virtual, por lo que los nombres de las VM tienen el formato de hello `<computerNamePrefix>_<auto-generated-index>`.</span><span class="sxs-lookup"><span data-stu-id="46543-170">hello scale set appends an index toohello prefix for each VM, so VM names have hello form `<computerNamePrefix>_<auto-generated-index>`.</span></span>

<span data-ttu-id="46543-171">En hello siguiente fragmento de código, utilizamos parámetros Hola de antes de tooset Hola administrador username y password para todas las máquinas virtuales en el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="46543-171">In hello following snippet, we use hello parameters from before tooset hello administrator username and password for all VMs in hello scale set.</span></span> <span data-ttu-id="46543-172">Hacer esto con hello `parameters` función de plantilla.</span><span class="sxs-lookup"><span data-stu-id="46543-172">We do this with hello `parameters` template function.</span></span> <span data-ttu-id="46543-173">Esta función toma una cadena que especifica qué tooand toorefer de parámetro genera el valor de Hola para ese parámetro.</span><span class="sxs-lookup"><span data-stu-id="46543-173">This function takes in a string that specifies which parameter toorefer tooand outputs hello value for that parameter.</span></span>

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a><span data-ttu-id="46543-174">Especificación de la red de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="46543-174">Specify VM network configuration</span></span>
<span data-ttu-id="46543-175">Por último, necesitamos toospecify configuración de red de Hola para máquinas virtuales de hello en el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="46543-175">Finally, we need toospecify hello network configuration for hello VMs in hello scale set.</span></span> <span data-ttu-id="46543-176">En este caso, únicamente se necesita toospecify Hola identificador de subred de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="46543-176">In this case, we only need toospecify hello ID of hello subnet created earlier.</span></span> <span data-ttu-id="46543-177">Esto indica a escala Hola establece tooput interfaces de red de hello en esta subred.</span><span class="sxs-lookup"><span data-stu-id="46543-177">This tells hello scale set tooput hello network interfaces in this subnet.</span></span>

<span data-ttu-id="46543-178">Puede obtener Id. de Hola de red virtual de Hola que contiene la subred de hello mediante el uso de hello `resourceId` función de plantilla.</span><span class="sxs-lookup"><span data-stu-id="46543-178">You can get hello ID of hello virtual network containing hello subnet by using hello `resourceId` template function.</span></span> <span data-ttu-id="46543-179">Esta función toma el tipo de Hola y el nombre de un recurso y devuelve Hola identificador completo de ese recurso.</span><span class="sxs-lookup"><span data-stu-id="46543-179">This function takes in hello type and name of a resource and returns hello fully qualified identifier of that resource.</span></span> <span data-ttu-id="46543-180">Este identificador tiene forma de hello:`/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span><span class="sxs-lookup"><span data-stu-id="46543-180">This ID has hello form: `/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span></span>

<span data-ttu-id="46543-181">Sin embargo, identificador de Hola de red virtual de hello no es suficiente.</span><span class="sxs-lookup"><span data-stu-id="46543-181">However, hello identifier of hello virtual network is not enough.</span></span> <span data-ttu-id="46543-182">Debe especificar la subred específica de Hola que Hola máquinas virtuales deben estar en el conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="46543-182">You must specify hello specific subnet that hello scale set VMs should be in.</span></span> <span data-ttu-id="46543-183">toodo, concatenar `/subnets/mySubnet` toohello identificador de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="46543-183">toodo this, concatenate `/subnets/mySubnet` toohello ID of hello virtual network.</span></span> <span data-ttu-id="46543-184">resultado de Hello es Id. de hello completo de la subred de Hola.</span><span class="sxs-lookup"><span data-stu-id="46543-184">hello result is hello fully qualified ID of hello subnet.</span></span> <span data-ttu-id="46543-185">Realice esta concatenación con hello `concat` función, que toma una serie de cadenas y devuelve su concatenación.</span><span class="sxs-lookup"><span data-stu-id="46543-185">Do this concatenation with hello `concat` function, which takes in a series of strings and returns their concatenation.</span></span>

```json
           "networkProfile": {
             "networkInterfaceConfigurations": [
               {
                 "name": "myNic",
                 "properties": {
                   "primary": "true",
                   "ipConfigurations": [
                     {
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
                           "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
                         }
                       }
                     }
                   ]
                 }
               }
             ]
           }
         }
       }
     }
   ]
}

```

## <a name="next-steps"></a><span data-ttu-id="46543-186">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="46543-186">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
