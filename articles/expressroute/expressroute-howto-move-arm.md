---
title: "Transición de circuitos ExpressRoute desde el modelo de implementación clásica al modelo de implementación de Resource Manager mediante PowerShell y Azure | Microsoft Docs"
description: "En esta página se describe cómo mover un circuito clásico al modelo de implementación de Resource Manager mediante PowerShell."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 08152836-23e7-42d1-9a56-8306b341cd91
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/03/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: c407e01e6d881cb8adcfe55faa246468669be883
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="move-expressroute-circuits-from-the-classic-to-the-resource-manager-deployment-model-using-powershell"></a><span data-ttu-id="99164-103">Transición de los circuitos ExpressRoute desde el modelo de implementación clásica al modelo de implementación de Resource Manager mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="99164-103">Move ExpressRoute circuits from the classic to the Resource Manager deployment model using PowerShell</span></span>

<span data-ttu-id="99164-104">Para usar un circuito ExpressRoute con el modelo de implementación clásica y el modelo de implementación de Resource Manager, debe mover el circuito al modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="99164-104">To use an ExpressRoute circuit for both the classic and Resource Manager deployment models, you must move the circuit to the Resource Manager deployment model.</span></span> <span data-ttu-id="99164-105">Las siguientes secciones le ayudan a mover su circuito mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="99164-105">The following sections help you move your circuit by using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="99164-106">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="99164-106">Before you begin</span></span>

* <span data-ttu-id="99164-107">Compruebe que dispone de la versión más reciente de los módulos de Azure PowerShell (como mínimo, la versión 1.0).</span><span class="sxs-lookup"><span data-stu-id="99164-107">Verify that you have the latest version of the Azure PowerShell modules (at least version 1.0).</span></span> <span data-ttu-id="99164-108">Para más información, vea [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="99164-108">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="99164-109">Asegúrese de haber revisado los [requisitos previos](expressroute-prerequisites.md), los [requisitos de enrutamiento](expressroute-routing.md) y los [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="99164-109">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="99164-110">Revise la información que se proporciona en [Transición de un circuito ExpressRoute desde la implementación clásica a la implementación de Resource Manager](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="99164-110">Review the information that is provided under [Moving an ExpressRoute circuit from classic to Resource Manager](expressroute-move.md).</span></span> <span data-ttu-id="99164-111">Asegúrese de que comprende perfectamente los límites y restricciones.</span><span class="sxs-lookup"><span data-stu-id="99164-111">Make sure that you fully understand the limits and limitations.</span></span>
* <span data-ttu-id="99164-112">Compruebe que el circuito está totalmente operativo en el modelo de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="99164-112">Verify that the circuit is fully operational in the classic deployment model.</span></span>
* <span data-ttu-id="99164-113">Asegúrese de tener un grupo de recursos creado en el modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="99164-113">Ensure that you have a resource group that was created in the Resource Manager deployment model.</span></span>

## <a name="move-an-expressroute-circuit"></a><span data-ttu-id="99164-114">Movimiento de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="99164-114">Move an ExpressRoute circuit</span></span>

### <a name="step-1-gather-circuit-details-from-the-classic-deployment-model"></a><span data-ttu-id="99164-115">Paso 1: Recopile detalles del circuito desde el modelo de implementación clásica</span><span class="sxs-lookup"><span data-stu-id="99164-115">Step 1: Gather circuit details from the classic deployment model</span></span>

<span data-ttu-id="99164-116">Inicie sesión en el entorno clásico de Azure y recopile la clave de servicio.</span><span class="sxs-lookup"><span data-stu-id="99164-116">Sign in to the Azure classic environment and gather the service key.</span></span>

1. <span data-ttu-id="99164-117">Inicie sesión en la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="99164-117">Sign in to your Azure account.</span></span>

  ```powershell
  Add-AzureAccount
  ```

2. <span data-ttu-id="99164-118">Seleccione la suscripción de Azure apropiada.</span><span class="sxs-lookup"><span data-stu-id="99164-118">Select the appropriate Azure subscription.</span></span>

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. <span data-ttu-id="99164-119">Importe los módulos de PowerShell para Azure y ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="99164-119">Import the PowerShell modules for Azure and ExpressRoute.</span></span>

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. <span data-ttu-id="99164-120">Use el cmdlet siguiente para obtener las claves de servicio de todos los circuitos ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="99164-120">Use the cmdlet below to get the service keys for all of your ExpressRoute circuits.</span></span> <span data-ttu-id="99164-121">Después de recuperar las claves, copie la **clave de servicio** del circuito que desea mover al modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="99164-121">After retrieving the keys, copy the **service key** of the circuit that you want to move to the Resource Manager deployment model.</span></span>

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a><span data-ttu-id="99164-122">Paso 2: Inicio de sesión y creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="99164-122">Step 2: Sign in and create a resource group</span></span>

<span data-ttu-id="99164-123">Inicie sesión en el entorno de Resource Manager y cree un grupo de recursos nuevo.</span><span class="sxs-lookup"><span data-stu-id="99164-123">Sign in to the Resource Manager environment and create a new resource group.</span></span>

1. <span data-ttu-id="99164-124">Inicie sesión en el entorno de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="99164-124">Sign in to your Azure Resource Manager environment.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="99164-125">Seleccione la suscripción de Azure apropiada.</span><span class="sxs-lookup"><span data-stu-id="99164-125">Select the appropriate Azure subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. <span data-ttu-id="99164-126">Modifique el fragmento de código siguiente para crear un nuevo grupo de recursos si aún no lo tiene.</span><span class="sxs-lookup"><span data-stu-id="99164-126">Modify the snippet below to create a new resource group if you don't already have a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-the-expressroute-circuit-to-the-resource-manager-deployment-model"></a><span data-ttu-id="99164-127">Paso 3: Mover el circuito ExpressRoute al modelo de implementación de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="99164-127">Step 3: Move the ExpressRoute circuit to the Resource Manager deployment model</span></span>

<span data-ttu-id="99164-128">Ya está listo para mover el circuito ExpressRoute desde el modelo de implementación clásica al modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="99164-128">You are now ready to move your ExpressRoute circuit from the classic deployment model to the Resource Manager deployment model.</span></span> <span data-ttu-id="99164-129">Antes de continuar, revise la información que se proporciona en [Transición de un circuito ExpressRoute desde el modelo de implementación clásica al modelo de implementación de Resource Manager](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="99164-129">Before proceeding, review the information provided in [Moving an ExpressRoute circuit from the classic to the Resource Manager deployment model](expressroute-move.md).</span></span>

<span data-ttu-id="99164-130">Para mover el circuito, modifique y ejecute el siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="99164-130">To move your circuit, modify and run the following snippet:</span></span>

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> <span data-ttu-id="99164-131">Una vez que se termine la transición, se usará el nombre nuevo que aparece en el cmdlet anterior para referirse al recurso.</span><span class="sxs-lookup"><span data-stu-id="99164-131">After the move has finished, the new name that is listed in the previous cmdlet will be used to address the resource.</span></span> <span data-ttu-id="99164-132">Básicamente, se cambiará el nombre del circuito.</span><span class="sxs-lookup"><span data-stu-id="99164-132">The circuit will essentially be renamed.</span></span>
> 

## <a name="modify-circuit-access"></a><span data-ttu-id="99164-133">Modificación del acceso al circuito</span><span class="sxs-lookup"><span data-stu-id="99164-133">Modify circuit access</span></span>

### <a name="to-enable-expressroute-circuit-access-for-both-deployment-models"></a><span data-ttu-id="99164-134">Habilitación del acceso al circuito ExpressRoute para ambos modelos de implementación</span><span class="sxs-lookup"><span data-stu-id="99164-134">To enable ExpressRoute circuit access for both deployment models</span></span>

<span data-ttu-id="99164-135">Después de mover el circuito ExpressRoute creado con el modelo clásico al modelo de implementación de Resource Manager, puede habilitar el acceso a ambos modelos de implementación.</span><span class="sxs-lookup"><span data-stu-id="99164-135">After moving your classic ExpressRoute circuit to the Resource Manager deployment model, you can enable access to both deployment models.</span></span> <span data-ttu-id="99164-136">Ejecute el siguiente cmdlet para habilitar el acceso a ambos modelos de implementación:</span><span class="sxs-lookup"><span data-stu-id="99164-136">Run the following cmdlets to enable access to both deployment models:</span></span>

1. <span data-ttu-id="99164-137">Obtenga los detalles del circuito.</span><span class="sxs-lookup"><span data-stu-id="99164-137">Get the circuit details.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="99164-138">Establezca "Allow Classic Operations" (Permitir operaciones clásicas) en TRUE.</span><span class="sxs-lookup"><span data-stu-id="99164-138">Set "Allow Classic Operations" to TRUE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. <span data-ttu-id="99164-139">Actualice el circuito.</span><span class="sxs-lookup"><span data-stu-id="99164-139">Update the circuit.</span></span> <span data-ttu-id="99164-140">Una vez que esta operación finalice correctamente, podrá ver el circuito en el modelo de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="99164-140">After this operation has finished successfully, you will be able to view the circuit in the classic deployment model.</span></span>

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. <span data-ttu-id="99164-141">Ejecute el siguiente cmdlet para obtener los detalles del circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="99164-141">Run the following cmdlet to get the details of the ExpressRoute circuit.</span></span> <span data-ttu-id="99164-142">También debe poder ver la clave de servicio.</span><span class="sxs-lookup"><span data-stu-id="99164-142">You must be able to see the service key listed.</span></span>

  ```powershell
  get-azurededicatedcircuit
  ```

5. <span data-ttu-id="99164-143">Ahora puede administrar los vínculos al circuito ExpressRoute mediante los comandos del modelo de implementación clásica para redes virtuales clásicas y los comandos del modelo de implementación de Resource Manager para redes virtuales de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="99164-143">You can now manage links to the ExpressRoute circuit using the classic deployment model commands for classic VNets, and the Resource Manager commands for Resource Manager VNets.</span></span> <span data-ttu-id="99164-144">Los artículos siguientes le ayudan a administrar los vínculos al circuito ExpressRoute:</span><span class="sxs-lookup"><span data-stu-id="99164-144">The following articles help you manage links to the ExpressRoute circuit:</span></span>

    * [<span data-ttu-id="99164-145">Vinculación de redes virtuales a circuitos ExpressRoute en el modelo de implementación de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="99164-145">Link your virtual network to your ExpressRoute circuit in the Resource Manager deployment model</span></span>](expressroute-howto-linkvnet-arm.md)
    * [<span data-ttu-id="99164-146">Vinculación de redes virtuales a circuitos ExpressRoute en el modelo de implementación clásica</span><span class="sxs-lookup"><span data-stu-id="99164-146">Link your virtual network to your ExpressRoute circuit in the classic deployment model</span></span>](expressroute-howto-linkvnet-classic.md)

### <a name="to-disable-expressroute-circuit-access-to-the-classic-deployment-model"></a><span data-ttu-id="99164-147">Deshabilitación del acceso al circuito ExpressRoute en el modelo de implementación clásica</span><span class="sxs-lookup"><span data-stu-id="99164-147">To disable ExpressRoute circuit access to the classic deployment model</span></span>

<span data-ttu-id="99164-148">Ejecute los siguientes cmdlets para deshabilitar el acceso al modelo de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="99164-148">Run the following cmdlets to disable access to the classic deployment model.</span></span>

1. <span data-ttu-id="99164-149">Obtenga los detalles del circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="99164-149">Get details of the ExpressRoute circuit.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="99164-150">Establezca "Allow Classic Operations" (Permitir operaciones clásicas) en FALSE.</span><span class="sxs-lookup"><span data-stu-id="99164-150">Set "Allow Classic Operations" to FALSE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. <span data-ttu-id="99164-151">Actualice el circuito.</span><span class="sxs-lookup"><span data-stu-id="99164-151">Update the circuit.</span></span> <span data-ttu-id="99164-152">Una vez que esta operación finalice correctamente, no podrá ver el circuito en el modelo de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="99164-152">After this operation has finished successfully, you will not be able to view the circuit in the classic deployment model.</span></span>

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a><span data-ttu-id="99164-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="99164-153">Next steps</span></span>

* [<span data-ttu-id="99164-154">Crear y modificar el enrutamiento para el circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="99164-154">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="99164-155">Vincular la red virtual a su circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="99164-155">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)