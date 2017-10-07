---
title: "listas de control de acceso al extremo de Azure aaaManage | PowerShell | Clásico | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage ACL con PowerShell"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c84e40af-f351-4572-b3f0-d572d46bafe7
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a7ca241ea108a266085bfb689b742d781e58da1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-endpoint-access-control-lists-using-powershell-in-hello-classic-deployment-model"></a><span data-ttu-id="fadcf-103">Administrar listas de control de acceso de punto de conexión mediante PowerShell en el modelo de implementación clásica de Hola</span><span class="sxs-lookup"><span data-stu-id="fadcf-103">Manage endpoint access control lists using PowerShell in hello classic deployment model</span></span>
<span data-ttu-id="fadcf-104">Puede crear y administrar listas de Control de acceso (ACL) de red para extremos usando Azure PowerShell o en hello Portal de administración.</span><span class="sxs-lookup"><span data-stu-id="fadcf-104">You can create and manage Network Access Control Lists (ACLs) for endpoints by using Azure PowerShell or in hello Management Portal.</span></span> <span data-ttu-id="fadcf-105">En este tema, encontrará procedimientos para realizar tareas comunes de ACL mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fadcf-105">In this topic, you'll find procedures for ACL common tasks that you can complete using PowerShell.</span></span> <span data-ttu-id="fadcf-106">Hola Consulte lista de Azure PowerShell cmdlets [Cmdlets de administración de Azure](http://go.microsoft.com/fwlink/?LinkId=317721).</span><span class="sxs-lookup"><span data-stu-id="fadcf-106">For hello list of Azure PowerShell cmdlets see [Azure Management Cmdlets](http://go.microsoft.com/fwlink/?LinkId=317721).</span></span> <span data-ttu-id="fadcf-107">Para obtener más información acerca de las ACL, consulte [Acerca de las listas de control de acceso (ACL) de red](virtual-networks-acl.md).</span><span class="sxs-lookup"><span data-stu-id="fadcf-107">For more information about ACLs, see [What is a Network Access Control List (ACL)?](virtual-networks-acl.md).</span></span> <span data-ttu-id="fadcf-108">Si desea toomanage su ACL mediante el uso de hello Portal de administración, consulte [cómo tooSet extremos tooa Máquina Virtual](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fadcf-108">If you want toomanage your ACLs by using hello Management Portal, see [How tooSet Up Endpoints tooa Virtual Machine](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="manage-network-acls-by-using-azure-powershell"></a><span data-ttu-id="fadcf-109">Administrar las ACL de red mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fadcf-109">Manage Network ACLs by using Azure PowerShell</span></span>
<span data-ttu-id="fadcf-110">Puede utilizar toocreate de cmdlets de PowerShell de Azure, quitar y configurar (establecer) listas de Control de acceso (ACL) de red.</span><span class="sxs-lookup"><span data-stu-id="fadcf-110">You can use Azure PowerShell cmdlets toocreate, remove, and configure (set) Network Access Control Lists (ACLs).</span></span> <span data-ttu-id="fadcf-111">Hemos incluido ejemplos de algunas maneras de hello que puede configurar una ACL mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fadcf-111">We've included a few examples of some of hello ways you can configure an ACL using PowerShell.</span></span>

<span data-ttu-id="fadcf-112">tooretrieve obtener una lista completa de cmdlets de PowerShell de ACL de hello, puede utilizar cualquiera de los siguientes Hola:</span><span class="sxs-lookup"><span data-stu-id="fadcf-112">tooretrieve a complete list of hello ACL PowerShell cmdlets, you can use either of hello following:</span></span>

    Get-Help *AzureACL*
    Get-Command -Noun AzureACLConfig

### <a name="create-a-network-acl-with-rules-that-permit-access-from-a-remote-subnet"></a><span data-ttu-id="fadcf-113">Crear una ACL de red con reglas que permitan el acceso desde una subred remota</span><span class="sxs-lookup"><span data-stu-id="fadcf-113">Create a Network ACL with rules that permit access from a remote subnet</span></span>
<span data-ttu-id="fadcf-114">ejemplo de Hola siguiente ilustra un toocreate forma una nueva ACL que contiene las reglas.</span><span class="sxs-lookup"><span data-stu-id="fadcf-114">hello example below illustrates a way toocreate a new ACL that contains rules.</span></span> <span data-ttu-id="fadcf-115">A continuación, se aplica esta ACL tooa extremo de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fadcf-115">This ACL is then applied tooa virtual machine endpoint.</span></span> <span data-ttu-id="fadcf-116">las reglas de ACL de Hello en el siguiente ejemplo de Hola permitirá el acceso desde una subred remota.</span><span class="sxs-lookup"><span data-stu-id="fadcf-116">hello ACL rules in hello example below will allow access from a remote subnet.</span></span> <span data-ttu-id="fadcf-117">toocreate una nueva ACL de red con reglas de permiso para una subred remota, abra un ISE de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="fadcf-117">toocreate a new Network ACL with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="fadcf-118">Copie y pegue el script de Hola a continuación, configurar script de Hola con sus propios valores y, a continuación, ejecute el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="fadcf-118">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

1. <span data-ttu-id="fadcf-119">Crear el nuevo objeto de ACL de red Hola.</span><span class="sxs-lookup"><span data-stu-id="fadcf-119">Create hello new network ACL object.</span></span>
   
        $acl1 = New-AzureAclConfig
2. <span data-ttu-id="fadcf-120">Establezca una regla que permita el acceso desde una subred remota.</span><span class="sxs-lookup"><span data-stu-id="fadcf-120">Set a rule that permits access from a remote subnet.</span></span> <span data-ttu-id="fadcf-121">En el ejemplo de Hola a continuación, establecer reglas *100* (que tiene prioridad sobre la regla 200 y versiones posterior) subred remota de hello tooallow *10.0.0.0/8* acceso toohello extremo de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fadcf-121">In hello example below, you set rule *100* (which has priority over rule 200 and higher) tooallow hello remote subnet *10.0.0.0/8* access toohello virtual machine endpoint.</span></span> <span data-ttu-id="fadcf-122">Reemplace los valores de hello con sus propios requisitos de configuración.</span><span class="sxs-lookup"><span data-stu-id="fadcf-122">Replace hello values with your own configuration requirements.</span></span> <span data-ttu-id="fadcf-123">nombre de Hola "SharePoint ACL config" debe reemplazarse con el nombre descriptivo de Hola que desea toocall esta regla.</span><span class="sxs-lookup"><span data-stu-id="fadcf-123">hello name "SharePoint ACL config" should be replaced with hello friendly name that you want toocall this rule.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "SharePoint ACL config"
3. <span data-ttu-id="fadcf-124">Para otras reglas adicionales, repita el cmdlet hello, reemplazando los valores de hello con sus propios requisitos de configuración.</span><span class="sxs-lookup"><span data-stu-id="fadcf-124">For additional rules, repeat hello cmdlet, replacing hello values with your own configuration requirements.</span></span> <span data-ttu-id="fadcf-125">Ser seguro toochange Hola regla número tooreflect Hola pedido en el que desea Hola reglas toobe aplicado.</span><span class="sxs-lookup"><span data-stu-id="fadcf-125">Be sure toochange hello rule number Order tooreflect hello order in which you want hello rules toobe applied.</span></span> <span data-ttu-id="fadcf-126">número de regla de Hello menor tiene prioridad sobre número mayor de Hola.</span><span class="sxs-lookup"><span data-stu-id="fadcf-126">hello lower rule number takes precedence over hello higher number.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
4. <span data-ttu-id="fadcf-127">A continuación, puede crear un nuevo extremo (Add) o establecer hello ACL para un extremo existente (Set).</span><span class="sxs-lookup"><span data-stu-id="fadcf-127">Next, you can either create a new endpoint (Add) or set hello ACL for an existing endpoint (Set).</span></span> <span data-ttu-id="fadcf-128">En este ejemplo, agregaremos que un nuevo extremo de máquina virtual denominado "web" y actualizar extremo de máquina virtual de hello con hello configuración de ACL.</span><span class="sxs-lookup"><span data-stu-id="fadcf-128">In this example, we will add a new virtual machine endpoint called "web" and update hello virtual machine endpoint with hello ACL settings.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        | Update-AzureVM
5. <span data-ttu-id="fadcf-129">A continuación, combinar los cmdlets de Hola y ejecute el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="fadcf-129">Next, combine hello cmdlets and run hello script.</span></span> <span data-ttu-id="fadcf-130">En este ejemplo, hello cmdlets combinados sería similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="fadcf-130">For this example, hello combined cmdlets would look like this:</span></span>
   
        $acl1 = New-AzureAclConfig
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "Sharepoint ACL config"
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        |Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        |Update-AzureVM

### <a name="remove-a-network-acl-rule-that-permits-access-from-a-remote-subnet"></a><span data-ttu-id="fadcf-131">Quitar una regla de ACL de red que permita el acceso desde una subred remota</span><span class="sxs-lookup"><span data-stu-id="fadcf-131">Remove a Network ACL rule that permits access from a remote subnet</span></span>
<span data-ttu-id="fadcf-132">ejemplo de Hola siguiente ilustra un tooremove forma una regla de ACL de red.</span><span class="sxs-lookup"><span data-stu-id="fadcf-132">hello example below illustrates a way tooremove a network ACL rule.</span></span>  <span data-ttu-id="fadcf-133">reglas de tooremove una regla de ACL de red con permiso para una subred remota, abra un ISE de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="fadcf-133">tooremove a Network ACL rule with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="fadcf-134">Copie y pegue el script de Hola a continuación, configurar script de Hola con sus propios valores y, a continuación, ejecute el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="fadcf-134">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

1. <span data-ttu-id="fadcf-135">Primer paso es objeto de ACL de red tooget hello para el extremo de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="fadcf-135">First step is tooget hello Network ACL object for hello virtual machine endpoint.</span></span> <span data-ttu-id="fadcf-136">A continuación, podrá quitar regla de ACL de Hola.</span><span class="sxs-lookup"><span data-stu-id="fadcf-136">You'll then remove hello ACL rule.</span></span> <span data-ttu-id="fadcf-137">En este caso, la estamos quitando por el identificador de regla.</span><span class="sxs-lookup"><span data-stu-id="fadcf-137">In this case, we are removing it by rule ID.</span></span> <span data-ttu-id="fadcf-138">Esto solo quitará Hola de Id. de regla 0 de hello ACL.</span><span class="sxs-lookup"><span data-stu-id="fadcf-138">This will only remove hello rule ID 0 from hello ACL.</span></span> <span data-ttu-id="fadcf-139">No elimina el objeto de ACL de Hola de extremo de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="fadcf-139">It does not remove hello ACL object from hello virtual machine endpoint.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Get-AzureAclConfig –EndpointName "web" `
        | Set-AzureAclConfig –RemoveRule –ID 0 –ACL $acl1
2. <span data-ttu-id="fadcf-140">A continuación, debe aplicar el extremo de máquina virtual de toohello de objeto de ACL de red de Hola y actualizar la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="fadcf-140">Next, you must apply hello Network ACL object toohello virtual machine endpoint and update hello virtual machine.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Set-AzureEndpoint –ACL $acl1 –Name "web" `
        | Update-AzureVM

### <a name="remove-a-network-acl-from-a-virtual-machine-endpoint"></a><span data-ttu-id="fadcf-141">Quitar una ACL de red de un extremo de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="fadcf-141">Remove a Network ACL from a virtual machine endpoint</span></span>
<span data-ttu-id="fadcf-142">En determinados escenarios, conviene tooremove un objeto de ACL de red desde un punto de conexión de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fadcf-142">In certain scenarios, you might want tooremove a Network ACL object from a virtual machine endpoint.</span></span> <span data-ttu-id="fadcf-143">toodo que abra un ISE de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="fadcf-143">toodo that, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="fadcf-144">Copie y pegue el script de Hola a continuación, configurar script de Hola con sus propios valores y, a continuación, ejecute el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="fadcf-144">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Remove-AzureAclConfig –EndpointName "web" `
        | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="fadcf-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fadcf-145">Next steps</span></span>
[<span data-ttu-id="fadcf-146">¿Qué es una lista de control de acceso (ACL) de red?</span><span class="sxs-lookup"><span data-stu-id="fadcf-146">What is a Network Access Control List (ACL)?</span></span>](virtual-networks-acl.md)

