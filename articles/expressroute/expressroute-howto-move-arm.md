---
title: "Mover los circuitos ExpressRoute de tooResource clásico Manager: PowerShell: Azure | Documentos de Microsoft"
description: "Esta página describe cómo toomove una toohello de circuito clásico implementación del Administrador de recursos del modelo mediante PowerShell."
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
ms.openlocfilehash: 8dcadafca5e4f40773902cec5786eba1dbe133eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model-using-powershell"></a><span data-ttu-id="e8d17-103">Mover los circuitos ExpressRoute de modelo de implementación de administrador de recursos hello toohello clásico con PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8d17-103">Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model using PowerShell</span></span>

<span data-ttu-id="e8d17-104">toouse un circuito de ExpressRoute para hello clásico y modelos de implementación del Administrador de recursos, debe mover el modelo de implementación de hello circuito toohello el Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="e8d17-104">toouse an ExpressRoute circuit for both hello classic and Resource Manager deployment models, you must move hello circuit toohello Resource Manager deployment model.</span></span> <span data-ttu-id="e8d17-105">Hello las secciones siguientes se ayuda a adoptar el circuito usando PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e8d17-105">hello following sections help you move your circuit by using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e8d17-106">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="e8d17-106">Before you begin</span></span>

* <span data-ttu-id="e8d17-107">Compruebe que tiene la versión más reciente de Hola de módulos de PowerShell de Azure de hello (al menos la versión 1.0).</span><span class="sxs-lookup"><span data-stu-id="e8d17-107">Verify that you have hello latest version of hello Azure PowerShell modules (at least version 1.0).</span></span> <span data-ttu-id="e8d17-108">Para obtener más información, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e8d17-108">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="e8d17-109">Asegúrese de que ha revisado hello [requisitos previos](expressroute-prerequisites.md), [requisitos de enrutamiento](expressroute-routing.md), y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="e8d17-109">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="e8d17-110">Revise la información de Hola que se proporciona en [mover un circuito de ExpressRoute de tooResource clásico Manager](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="e8d17-110">Review hello information that is provided under [Moving an ExpressRoute circuit from classic tooResource Manager](expressroute-move.md).</span></span> <span data-ttu-id="e8d17-111">Asegúrese de que entiende totalmente Hola límites y limitaciones.</span><span class="sxs-lookup"><span data-stu-id="e8d17-111">Make sure that you fully understand hello limits and limitations.</span></span>
* <span data-ttu-id="e8d17-112">Compruebe que el circuito de hello es totalmente operativo en el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8d17-112">Verify that hello circuit is fully operational in hello classic deployment model.</span></span>
* <span data-ttu-id="e8d17-113">Asegúrese de que tiene un grupo de recursos que se creó en el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8d17-113">Ensure that you have a resource group that was created in hello Resource Manager deployment model.</span></span>

## <a name="move-an-expressroute-circuit"></a><span data-ttu-id="e8d17-114">Movimiento de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e8d17-114">Move an ExpressRoute circuit</span></span>

### <a name="step-1-gather-circuit-details-from-hello-classic-deployment-model"></a><span data-ttu-id="e8d17-115">Paso 1: Recopilar detalles del circuito de modelo de implementación clásica de Hola</span><span class="sxs-lookup"><span data-stu-id="e8d17-115">Step 1: Gather circuit details from hello classic deployment model</span></span>

<span data-ttu-id="e8d17-116">Inicie sesión en toohello el entorno clásico de Azure y obtener la clave de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8d17-116">Sign in toohello Azure classic environment and gather hello service key.</span></span>

1. <span data-ttu-id="e8d17-117">Inicie sesión en tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="e8d17-117">Sign in tooyour Azure account.</span></span>

  ```powershell
  Add-AzureAccount
  ```

2. <span data-ttu-id="e8d17-118">Seleccione la suscripción a Azure apropiada Hola.</span><span class="sxs-lookup"><span data-stu-id="e8d17-118">Select hello appropriate Azure subscription.</span></span>

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. <span data-ttu-id="e8d17-119">Importar módulos de PowerShell de Hola de Azure y ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e8d17-119">Import hello PowerShell modules for Azure and ExpressRoute.</span></span>

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. <span data-ttu-id="e8d17-120">Usa el cmdlet Hola de claves para el servicio hello tooget para todos los circuitos ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e8d17-120">Use hello cmdlet below tooget hello service keys for all of your ExpressRoute circuits.</span></span> <span data-ttu-id="e8d17-121">Después de recuperar las claves de hello, copie hello **clave de servicio** de circuito de Hola que desea que el modelo de implementación de toomove toohello el Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="e8d17-121">After retrieving hello keys, copy hello **service key** of hello circuit that you want toomove toohello Resource Manager deployment model.</span></span>

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a><span data-ttu-id="e8d17-122">Paso 2: Inicio de sesión y creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="e8d17-122">Step 2: Sign in and create a resource group</span></span>

<span data-ttu-id="e8d17-123">Inicie sesión en el entorno de administrador de recursos de toohello y crear un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e8d17-123">Sign in toohello Resource Manager environment and create a new resource group.</span></span>

1. <span data-ttu-id="e8d17-124">Inicie sesión en el entorno de Azure Resource Manager tooyour.</span><span class="sxs-lookup"><span data-stu-id="e8d17-124">Sign in tooyour Azure Resource Manager environment.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="e8d17-125">Seleccione la suscripción a Azure apropiada Hola.</span><span class="sxs-lookup"><span data-stu-id="e8d17-125">Select hello appropriate Azure subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. <span data-ttu-id="e8d17-126">Modificar fragmento de código de hello debajo toocreate un nuevo grupo de recursos si aún no tiene un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e8d17-126">Modify hello snippet below toocreate a new resource group if you don't already have a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-hello-expressroute-circuit-toohello-resource-manager-deployment-model"></a><span data-ttu-id="e8d17-127">Paso 3: Mover el modelo de implementación de administrador de recursos de toohello circuito de ExpressRoute de Hola</span><span class="sxs-lookup"><span data-stu-id="e8d17-127">Step 3: Move hello ExpressRoute circuit toohello Resource Manager deployment model</span></span>

<span data-ttu-id="e8d17-128">Se está ahora listo toomove el circuito de ExpressRoute de modelo de implementación de administrador de recursos de toohello modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8d17-128">You are now ready toomove your ExpressRoute circuit from hello classic deployment model toohello Resource Manager deployment model.</span></span> <span data-ttu-id="e8d17-129">Antes de continuar, revise la información Hola proporcionada en [mover un circuito ExpressRoute de modelo de implementación de administrador de recursos de hello toohello clásico](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="e8d17-129">Before proceeding, review hello information provided in [Moving an ExpressRoute circuit from hello classic toohello Resource Manager deployment model](expressroute-move.md).</span></span>

<span data-ttu-id="e8d17-130">toomove el circuito, modifique y ejecute hello siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="e8d17-130">toomove your circuit, modify and run hello following snippet:</span></span>

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> <span data-ttu-id="e8d17-131">Cuando haya finalizado el movimiento de hello, nombre nuevo de Hola que aparece en el cmdlet anterior Hola será usado tooaddress Hola recursos.</span><span class="sxs-lookup"><span data-stu-id="e8d17-131">After hello move has finished, hello new name that is listed in hello previous cmdlet will be used tooaddress hello resource.</span></span> <span data-ttu-id="e8d17-132">Básicamente se cambiará el circuito de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8d17-132">hello circuit will essentially be renamed.</span></span>
> 

## <a name="modify-circuit-access"></a><span data-ttu-id="e8d17-133">Modificación del acceso al circuito</span><span class="sxs-lookup"><span data-stu-id="e8d17-133">Modify circuit access</span></span>

### <a name="tooenable-expressroute-circuit-access-for-both-deployment-models"></a><span data-ttu-id="e8d17-134">tooenable acceso de circuito de ExpressRoute para ambos modelos de implementación</span><span class="sxs-lookup"><span data-stu-id="e8d17-134">tooenable ExpressRoute circuit access for both deployment models</span></span>

<span data-ttu-id="e8d17-135">Después de mover el modelo de implementación en el Administrador de recursos de clásico ExpressRoute circuito toohello, puede habilitar los modelos de implementación de acceso tooboth.</span><span class="sxs-lookup"><span data-stu-id="e8d17-135">After moving your classic ExpressRoute circuit toohello Resource Manager deployment model, you can enable access tooboth deployment models.</span></span> <span data-ttu-id="e8d17-136">Ejecute hello después de modelos de implementación de cmdlets tooenable acceso tooboth:</span><span class="sxs-lookup"><span data-stu-id="e8d17-136">Run hello following cmdlets tooenable access tooboth deployment models:</span></span>

1. <span data-ttu-id="e8d17-137">Obtener detalles del circuito Hola.</span><span class="sxs-lookup"><span data-stu-id="e8d17-137">Get hello circuit details.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="e8d17-138">Establecer tooTRUE "Permitir operaciones clásico".</span><span class="sxs-lookup"><span data-stu-id="e8d17-138">Set "Allow Classic Operations" tooTRUE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. <span data-ttu-id="e8d17-139">Actualizar circuito Hola.</span><span class="sxs-lookup"><span data-stu-id="e8d17-139">Update hello circuit.</span></span> <span data-ttu-id="e8d17-140">Cuando esta operación ha finalizado correctamente, será capaz de tooview circuito de hello en el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8d17-140">After this operation has finished successfully, you will be able tooview hello circuit in hello classic deployment model.</span></span>

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. <span data-ttu-id="e8d17-141">Ejecute hello cmdlet tooget Hola detalla de hello circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e8d17-141">Run hello following cmdlet tooget hello details of hello ExpressRoute circuit.</span></span> <span data-ttu-id="e8d17-142">Debe ser toosee capaz de clave del servicio Hola enumerado.</span><span class="sxs-lookup"><span data-stu-id="e8d17-142">You must be able toosee hello service key listed.</span></span>

  ```powershell
  get-azurededicatedcircuit
  ```

5. <span data-ttu-id="e8d17-143">Ahora puede administrar el circuito de ExpressRoute de toohello vínculos mediante comandos de modelo de implementación clásica de Hola para redes virtuales clásicas y comandos del Administrador de recursos de hello para el Administrador de recursos VNets.</span><span class="sxs-lookup"><span data-stu-id="e8d17-143">You can now manage links toohello ExpressRoute circuit using hello classic deployment model commands for classic VNets, and hello Resource Manager commands for Resource Manager VNets.</span></span> <span data-ttu-id="e8d17-144">Hello artículos siguientes ayudarán a administrar vínculos toohello circuito de ExpressRoute:</span><span class="sxs-lookup"><span data-stu-id="e8d17-144">hello following articles help you manage links toohello ExpressRoute circuit:</span></span>

    * [<span data-ttu-id="e8d17-145">Vincular el circuito de ExpressRoute en el modelo de implementación del Administrador de recursos de hello tooyour de red virtual</span><span class="sxs-lookup"><span data-stu-id="e8d17-145">Link your virtual network tooyour ExpressRoute circuit in hello Resource Manager deployment model</span></span>](expressroute-howto-linkvnet-arm.md)
    * [<span data-ttu-id="e8d17-146">Vincular el circuito de ExpressRoute en el modelo de implementación clásica de hello tooyour de red virtual</span><span class="sxs-lookup"><span data-stu-id="e8d17-146">Link your virtual network tooyour ExpressRoute circuit in hello classic deployment model</span></span>](expressroute-howto-linkvnet-classic.md)

### <a name="toodisable-expressroute-circuit-access-toohello-classic-deployment-model"></a><span data-ttu-id="e8d17-147">modelo de implementación clásica de toohello de acceso circuito de ExpressRoute de toodisable</span><span class="sxs-lookup"><span data-stu-id="e8d17-147">toodisable ExpressRoute circuit access toohello classic deployment model</span></span>

<span data-ttu-id="e8d17-148">Ejecute hello siguiendo el modelo de implementación clásica de cmdlets toodisable acceso toohello.</span><span class="sxs-lookup"><span data-stu-id="e8d17-148">Run hello following cmdlets toodisable access toohello classic deployment model.</span></span>

1. <span data-ttu-id="e8d17-149">Obtener detalles de hello circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e8d17-149">Get details of hello ExpressRoute circuit.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="e8d17-150">Establecer tooFALSE "Permitir operaciones clásico".</span><span class="sxs-lookup"><span data-stu-id="e8d17-150">Set "Allow Classic Operations" tooFALSE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. <span data-ttu-id="e8d17-151">Actualizar circuito Hola.</span><span class="sxs-lookup"><span data-stu-id="e8d17-151">Update hello circuit.</span></span> <span data-ttu-id="e8d17-152">Después de esta operación ha finalizado correctamente, no será capaz de tooview circuito de hello en el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8d17-152">After this operation has finished successfully, you will not be able tooview hello circuit in hello classic deployment model.</span></span>

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a><span data-ttu-id="e8d17-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e8d17-153">Next steps</span></span>

* [<span data-ttu-id="e8d17-154">Crear y modificar el enrutamiento para el circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e8d17-154">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="e8d17-155">Vincular el circuito de ExpressRoute de tooyour de red virtual</span><span class="sxs-lookup"><span data-stu-id="e8d17-155">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
