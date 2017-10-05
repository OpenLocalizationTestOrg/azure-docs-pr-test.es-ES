---
title: "Administración de listas de control de acceso de puntos de conexión de Azure | PowerShell | Clásico | Microsoft Docs"
description: Aprenda a administrar las ACL con PowerShell
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
ms.openlocfilehash: c3476908447380ccd7e8b9c0f1c2a55ae763cc1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-endpoint-access-control-lists-using-powershell-in-the-classic-deployment-model"></a><span data-ttu-id="a9b6d-103">Administración de listas de control de acceso de puntos de conexión con PowerShell en el modelo de implementación clásico</span><span class="sxs-lookup"><span data-stu-id="a9b6d-103">Manage endpoint access control lists using PowerShell in the classic deployment model</span></span>
<span data-ttu-id="a9b6d-104">Puede crear y administrar listas de control de acceso (ACL) de red para extremos mediante Azure PowerShell o en el Portal de administración.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-104">You can create and manage Network Access Control Lists (ACLs) for endpoints by using Azure PowerShell or in the Management Portal.</span></span> <span data-ttu-id="a9b6d-105">En este tema, encontrará procedimientos para realizar tareas comunes de ACL mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-105">In this topic, you'll find procedures for ACL common tasks that you can complete using PowerShell.</span></span> <span data-ttu-id="a9b6d-106">Para obtener la lista de cmdlets de Azure PowerShell, consulte [Cmdlets de administración de Azure](http://go.microsoft.com/fwlink/?LinkId=317721).</span><span class="sxs-lookup"><span data-stu-id="a9b6d-106">For the list of Azure PowerShell cmdlets see [Azure Management Cmdlets](http://go.microsoft.com/fwlink/?LinkId=317721).</span></span> <span data-ttu-id="a9b6d-107">Para obtener más información acerca de las ACL, consulte [Acerca de las listas de control de acceso (ACL) de red](virtual-networks-acl.md).</span><span class="sxs-lookup"><span data-stu-id="a9b6d-107">For more information about ACLs, see [What is a Network Access Control List (ACL)?](virtual-networks-acl.md).</span></span> <span data-ttu-id="a9b6d-108">Si quiere administrar las ACL usando el Portal de administración, vea [Configuración de puntos de conexión en una máquina virtual de Windows clásica en Azure](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a9b6d-108">If you want to manage your ACLs by using the Management Portal, see [How to Set Up Endpoints to a Virtual Machine](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="manage-network-acls-by-using-azure-powershell"></a><span data-ttu-id="a9b6d-109">Administrar las ACL de red mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9b6d-109">Manage Network ACLs by using Azure PowerShell</span></span>
<span data-ttu-id="a9b6d-110">Puede usar cmdlets de Azure PowerShell para crear, quitar y configurar (establecer) listas de control de acceso (ACL) de red.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-110">You can use Azure PowerShell cmdlets to create, remove, and configure (set) Network Access Control Lists (ACLs).</span></span> <span data-ttu-id="a9b6d-111">Hemos incluido ejemplos de algunas de las formas en que puede configurar una ACL mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-111">We've included a few examples of some of the ways you can configure an ACL using PowerShell.</span></span>

<span data-ttu-id="a9b6d-112">Para recuperar una lista completa de los cmdlets de PowerShell para ACL, puede utilizar cualquiera de los cmdlets siguientes:</span><span class="sxs-lookup"><span data-stu-id="a9b6d-112">To retrieve a complete list of the ACL PowerShell cmdlets, you can use either of the following:</span></span>

    Get-Help *AzureACL*
    Get-Command -Noun AzureACLConfig

### <a name="create-a-network-acl-with-rules-that-permit-access-from-a-remote-subnet"></a><span data-ttu-id="a9b6d-113">Crear una ACL de red con reglas que permitan el acceso desde una subred remota</span><span class="sxs-lookup"><span data-stu-id="a9b6d-113">Create a Network ACL with rules that permit access from a remote subnet</span></span>
<span data-ttu-id="a9b6d-114">En el ejemplo siguiente se muestra una forma de crear una nueva ACL que contiene reglas.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-114">The example below illustrates a way to create a new ACL that contains rules.</span></span> <span data-ttu-id="a9b6d-115">Esta ACL se aplica después a un extremo de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-115">This ACL is then applied to a virtual machine endpoint.</span></span> <span data-ttu-id="a9b6d-116">Las reglas de ACL del ejemplo siguiente permitirán el acceso desde una subred remota.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-116">The ACL rules in the example below will allow access from a remote subnet.</span></span> <span data-ttu-id="a9b6d-117">Para crear una nueva ACL de red con reglas de permiso para una subred remota, abra un ISE de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-117">To create a new Network ACL with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="a9b6d-118">Copie y pegue el siguiente script, configure el script con sus propios valores y, a continuación, ejecute el script.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-118">Copy and paste the script below, configuring the script with your own values, and then run the script.</span></span>

1. <span data-ttu-id="a9b6d-119">Cree el nuevo objeto de ACL de red.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-119">Create the new network ACL object.</span></span>
   
        $acl1 = New-AzureAclConfig
2. <span data-ttu-id="a9b6d-120">Establezca una regla que permita el acceso desde una subred remota.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-120">Set a rule that permits access from a remote subnet.</span></span> <span data-ttu-id="a9b6d-121">En el ejemplo siguiente, se establece la regla *100* (que tiene prioridad sobre la regla 200 y otras superiores) para permitir el acceso de la subred remota *10.0.0.0/8* al punto de conexión de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-121">In the example below, you set rule *100* (which has priority over rule 200 and higher) to allow the remote subnet *10.0.0.0/8* access to the virtual machine endpoint.</span></span> <span data-ttu-id="a9b6d-122">Reemplace los valores con sus propios requisitos de configuración.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-122">Replace the values with your own configuration requirements.</span></span> <span data-ttu-id="a9b6d-123">El nombre “SharePoint ACL config” se debe reemplazar con el nombre descriptivo que desee asignar a esta regla.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-123">The name "SharePoint ACL config" should be replaced with the friendly name that you want to call this rule.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "SharePoint ACL config"
3. <span data-ttu-id="a9b6d-124">Para otras reglas adicionales, repita el cmdlet, reemplazando los valores con sus propios requisitos de configuración.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-124">For additional rules, repeat the cmdlet, replacing the values with your own configuration requirements.</span></span> <span data-ttu-id="a9b6d-125">Asegúrese de cambiar el orden del número de regla para reflejar el orden en que desea que se apliquen las reglas.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-125">Be sure to change the rule number Order to reflect the order in which you want the rules to be applied.</span></span> <span data-ttu-id="a9b6d-126">El número de regla menor tiene prioridad sobre el número mayor.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-126">The lower rule number takes precedence over the higher number.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
4. <span data-ttu-id="a9b6d-127">A continuación, puede crear un nuevo extremo (Add) o establecer la ACL para un extremo existente (Set).</span><span class="sxs-lookup"><span data-stu-id="a9b6d-127">Next, you can either create a new endpoint (Add) or set the ACL for an existing endpoint (Set).</span></span> <span data-ttu-id="a9b6d-128">En este ejemplo, agregaremos un nuevo extremo de máquina virtual denominado “web” y actualizaremos el extremo de máquina virtual con los valores de ACL.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-128">In this example, we will add a new virtual machine endpoint called "web" and update the virtual machine endpoint with the ACL settings.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        | Update-AzureVM
5. <span data-ttu-id="a9b6d-129">A continuación, combine los cmdlets y ejecute el script.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-129">Next, combine the cmdlets and run the script.</span></span> <span data-ttu-id="a9b6d-130">En este ejemplo, los cmdlets combinados serían similares a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a9b6d-130">For this example, the combined cmdlets would look like this:</span></span>
   
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

### <a name="remove-a-network-acl-rule-that-permits-access-from-a-remote-subnet"></a><span data-ttu-id="a9b6d-131">Quitar una regla de ACL de red que permita el acceso desde una subred remota</span><span class="sxs-lookup"><span data-stu-id="a9b6d-131">Remove a Network ACL rule that permits access from a remote subnet</span></span>
<span data-ttu-id="a9b6d-132">En el ejemplo siguiente se muestra una forma de quitar una regla de ACL de red.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-132">The example below illustrates a way to remove a network ACL rule.</span></span>  <span data-ttu-id="a9b6d-133">Para quitar una regla de ACL de red con reglas de permiso para una subred remota, abra un ISE de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-133">To remove a Network ACL rule with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="a9b6d-134">Copie y pegue el siguiente script, configure el script con sus propios valores y, a continuación, ejecute el script.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-134">Copy and paste the script below, configuring the script with your own values, and then run the script.</span></span>

1. <span data-ttu-id="a9b6d-135">El primer paso consiste en obtener el objeto de ACL de red para el extremo de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-135">First step is to get the Network ACL object for the virtual machine endpoint.</span></span> <span data-ttu-id="a9b6d-136">Después quitará la regla de ACL.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-136">You'll then remove the ACL rule.</span></span> <span data-ttu-id="a9b6d-137">En este caso, la estamos quitando por el identificador de regla.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-137">In this case, we are removing it by rule ID.</span></span> <span data-ttu-id="a9b6d-138">Esto solo quitará el identificador de regla 0 de la ACL.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-138">This will only remove the rule ID 0 from the ACL.</span></span> <span data-ttu-id="a9b6d-139">No quita el objeto de ACL del extremo de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-139">It does not remove the ACL object from the virtual machine endpoint.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Get-AzureAclConfig –EndpointName "web" `
        | Set-AzureAclConfig –RemoveRule –ID 0 –ACL $acl1
2. <span data-ttu-id="a9b6d-140">A continuación, debe aplicar el objeto de ACL de red al extremo de máquina virtual y actualizar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-140">Next, you must apply the Network ACL object to the virtual machine endpoint and update the virtual machine.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Set-AzureEndpoint –ACL $acl1 –Name "web" `
        | Update-AzureVM

### <a name="remove-a-network-acl-from-a-virtual-machine-endpoint"></a><span data-ttu-id="a9b6d-141">Quitar una ACL de red de un extremo de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="a9b6d-141">Remove a Network ACL from a virtual machine endpoint</span></span>
<span data-ttu-id="a9b6d-142">En ciertas situaciones, puede que desee quitar un objeto de ACL de red de un extremo de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-142">In certain scenarios, you might want to remove a Network ACL object from a virtual machine endpoint.</span></span> <span data-ttu-id="a9b6d-143">Para ello, abra un ISE de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-143">To do that, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="a9b6d-144">Copie y pegue el siguiente script, configure el script con sus propios valores y, a continuación, ejecute el script.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-144">Copy and paste the script below, configuring the script with your own values, and then run the script.</span></span>

        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Remove-AzureAclConfig –EndpointName "web" `
        | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="a9b6d-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a9b6d-145">Next steps</span></span>
[<span data-ttu-id="a9b6d-146">¿Qué es una lista de control de acceso (ACL) de red?</span><span class="sxs-lookup"><span data-stu-id="a9b6d-146">What is a Network Access Control List (ACL)?</span></span>](virtual-networks-acl.md)

