---
title: "una red virtual de Azure (clásica) con varias subredes aaaCreate | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una red virtual (clásica) con varias subredes en Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: cc7b9ad08d5c26dba09584762bedf614d2847032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a><span data-ttu-id="9d723-103">Creación de una red virtual (clásica) con varias subredes</span><span class="sxs-lookup"><span data-stu-id="9d723-103">Create a virtual network (classic) with multiple subnets</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9d723-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9d723-104">Azure has two [different deployment models](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) for creating and working with resources: Resource Manager and classic.</span></span> <span data-ttu-id="9d723-105">Este artículo incluye el uso de modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d723-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="9d723-106">Microsoft recomienda crear mayoría nuevas redes virtuales a través de hello [el Administrador de recursos](virtual-networks-create-vnet-arm-pportal.md) modelo de implementación.</span><span class="sxs-lookup"><span data-stu-id="9d723-106">Microsoft recommends creating most new virtual networks through hello [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) deployment model.</span></span>

<span data-ttu-id="9d723-107">En este tutorial, obtenga información acerca de cómo toocreate una básica red virtual de Azure (clásica) que tiene separar subredes públicas y privadas.</span><span class="sxs-lookup"><span data-stu-id="9d723-107">In this tutorial, learn how toocreate a basic Azure virtual network (classic) that has separate public and private subnets.</span></span> <span data-ttu-id="9d723-108">Puede crear recursos de Azure, como máquinas virtuales y servicios en la nube en una subred.</span><span class="sxs-lookup"><span data-stu-id="9d723-108">You can create Azure resources, like Virtual machines and Cloud services in a subnet.</span></span> <span data-ttu-id="9d723-109">Recursos creados en redes virtuales (clásicas) pueden comunicarse entre sí y con los recursos de otra red virtual conectado tooa de redes.</span><span class="sxs-lookup"><span data-stu-id="9d723-109">Resources created in virtual networks (classic) can communicate with each other, and with resources in other networks connected tooa virtual network.</span></span>

<span data-ttu-id="9d723-110">Más información sobre todos los valores de [red virtual](virtual-network-manage-network.md) y [subred](virtual-network-manage-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="9d723-110">Learn more about all [virtual network](virtual-network-manage-network.md) and [subnet](virtual-network-manage-subnet.md) settings.</span></span>

> [!WARNING]
> <span data-ttu-id="9d723-111">Azure elimina inmediatamente las redes virtuales (clásicas) cuando se [deshabilita una suscripción](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span><span class="sxs-lookup"><span data-stu-id="9d723-111">Virtual networks (classic) are immediately deleted by Azure when a [subscription is disabled](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span></span> <span data-ttu-id="9d723-112">Redes virtuales (clásicas) se eliminan independientemente de que existan los recursos de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d723-112">Virtual networks (classic) are deleted regardless of whether resources exist in hello virtual network.</span></span> <span data-ttu-id="9d723-113">Si más adelante vuelve a habilitar suscripción hello, se deben recrear los recursos que existían en la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d723-113">If you later re-enable hello subscription, resources that existed in hello virtual network must be recreated.</span></span>

<span data-ttu-id="9d723-114">Puede crear una red virtual (clásica) mediante hello [portal de Azure](#portal), hello [Azure interfaz de línea de comandos (CLI) 1.0](#azure-cli), o [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="9d723-114">You can create a virtual network (classic) by using hello [Azure portal](#portal), hello [Azure command-line interface (CLI) 1.0](#azure-cli), or [PowerShell](#powershell).</span></span>

## <a name="portal"></a><span data-ttu-id="9d723-115">Portal</span><span class="sxs-lookup"><span data-stu-id="9d723-115">Portal</span></span>

1. <span data-ttu-id="9d723-116">En un explorador de Internet, vaya toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9d723-116">In an Internet browser, go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9d723-117">Inicie sesión con la [cuenta de Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="9d723-117">Log in using your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="9d723-118">Si no tiene una cuenta de Azure, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="9d723-118">If you don't have an Azure account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="9d723-119">Haga clic en **+ nuevo** en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d723-119">Click **+New** in hello portal.</span></span>
3. <span data-ttu-id="9d723-120">Escriba *red Virtual* en hello **Hola búsqueda Marketplace** cuadro principio de Hola de hello **New** hoja que aparece.</span><span class="sxs-lookup"><span data-stu-id="9d723-120">Enter *Virtual network* in hello **Search hello Marketplace** box at hello top of hello **New** blade that appears.</span></span>  <span data-ttu-id="9d723-121">Haga clic en **red Virtual** cuando aparece en los resultados de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d723-121">Click **Virtual network** when it appears in hello search results.</span></span>
4. <span data-ttu-id="9d723-122">Seleccione **clásico** en hello **seleccionar un modelo de implementación** cuadro hello **red Virtual** hoja que aparece, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="9d723-122">Select **Classic** in hello **Select a deployment model** box in hello **Virtual Network** blade that appears, then click **Create**.</span></span> 
5. <span data-ttu-id="9d723-123">Escriba Hola siguiente valores de hello **crear red virtual (clásica)** hoja y, a continuación, haga clic en **crear**:</span><span class="sxs-lookup"><span data-stu-id="9d723-123">Enter hello following values on hello **Create virtual network (classic)** blade and then click **Create**:</span></span>

    |<span data-ttu-id="9d723-124">Configuración</span><span class="sxs-lookup"><span data-stu-id="9d723-124">Setting</span></span>|<span data-ttu-id="9d723-125">Valor</span><span class="sxs-lookup"><span data-stu-id="9d723-125">Value</span></span>|
    |---|---|
    |<span data-ttu-id="9d723-126">Nombre</span><span class="sxs-lookup"><span data-stu-id="9d723-126">Name</span></span>|<span data-ttu-id="9d723-127">myVnet</span><span class="sxs-lookup"><span data-stu-id="9d723-127">myVnet</span></span>|
    |<span data-ttu-id="9d723-128">Espacio de direcciones</span><span class="sxs-lookup"><span data-stu-id="9d723-128">Address space</span></span>|<span data-ttu-id="9d723-129">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="9d723-129">10.0.0.0/16</span></span>|
    |<span data-ttu-id="9d723-130">Nombre de subred</span><span class="sxs-lookup"><span data-stu-id="9d723-130">Subnet name</span></span>|<span data-ttu-id="9d723-131">Público</span><span class="sxs-lookup"><span data-stu-id="9d723-131">Public</span></span>|
    |<span data-ttu-id="9d723-132">Intervalo de direcciones de subred</span><span class="sxs-lookup"><span data-stu-id="9d723-132">Subnet address range</span></span>|<span data-ttu-id="9d723-133">10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="9d723-133">10.0.0.0/24</span></span>|
    |<span data-ttu-id="9d723-134">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="9d723-134">Resource group</span></span>|<span data-ttu-id="9d723-135">Deje seleccionado **Crear nuevo** y después escriba **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="9d723-135">Leave **Create new** selected, and then enter **myResourceGroup**.</span></span>|
    |<span data-ttu-id="9d723-136">Suscripción y ubicación</span><span class="sxs-lookup"><span data-stu-id="9d723-136">Subscription and location</span></span>|<span data-ttu-id="9d723-137">Seleccione su suscripción y ubicación.</span><span class="sxs-lookup"><span data-stu-id="9d723-137">Select your subscription and location.</span></span>

    <span data-ttu-id="9d723-138">Si es nuevo tooAzure, obtenga más información sobre [grupos de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [suscripciones](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), y [ubicaciones](https://azure.microsoft.com/regions) (también denominada tooas *regiones*).</span><span class="sxs-lookup"><span data-stu-id="9d723-138">If you're new tooAzure, learn more about [resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (also referred tooas *regions*).</span></span>
4. <span data-ttu-id="9d723-139">En el portal de hello, puede crear solo una subred cuando se crea una red virtual.</span><span class="sxs-lookup"><span data-stu-id="9d723-139">In hello portal, you can create only one subnet when you create a virtual network.</span></span> <span data-ttu-id="9d723-140">En este tutorial, creará una segunda subred después de crear la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d723-140">In this tutorial, you create a second subnet after you create hello virtual network.</span></span> <span data-ttu-id="9d723-141">Más adelante puede crear recursos accesibles desde Internet en hello **público** subred.</span><span class="sxs-lookup"><span data-stu-id="9d723-141">You might later create Internet-accessible resources in hello **Public** subnet.</span></span> <span data-ttu-id="9d723-142">También puede crear recursos que no son accesibles desde Internet de Hola Hola **privada** subred.</span><span class="sxs-lookup"><span data-stu-id="9d723-142">You also might create resources that aren't accessible from hello Internet in hello **Private** subnet.</span></span> <span data-ttu-id="9d723-143">toocreate Hola segunda subred, escriba **myVnet** en hello **buscar recursos** cuadro Hola principio de página Hola.</span><span class="sxs-lookup"><span data-stu-id="9d723-143">toocreate hello second subnet, enter **myVnet** in hello **Search resources** box at hello top of hello page.</span></span> <span data-ttu-id="9d723-144">Haga clic en **myVnet** cuando aparece en los resultados de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d723-144">Click **myVnet** when it appears in hello search results.</span></span>
5. <span data-ttu-id="9d723-145">Haga clic en **subredes** (Hola **configuración** sección) en hello **crear red virtual (clásica)** hoja que aparece.</span><span class="sxs-lookup"><span data-stu-id="9d723-145">Click **Subnets** (in hello **SETTINGS** section) on hello **Create virtual network (classic)** blade that appears.</span></span>
6. <span data-ttu-id="9d723-146">Haga clic en **+ agregar** en hello **myVnet - subredes** hoja que aparece.</span><span class="sxs-lookup"><span data-stu-id="9d723-146">Click **+Add** on hello **myVnet - Subnets** blade that appears.</span></span>
7. <span data-ttu-id="9d723-147">Escriba **privada** para **nombre** en hello **Agregar subred** hoja.</span><span class="sxs-lookup"><span data-stu-id="9d723-147">Enter **Private** for **Name** on hello **Add subnet** blade.</span></span> <span data-ttu-id="9d723-148">Especifique **10.0.1.0/24** para **Intervalo de direcciones**.</span><span class="sxs-lookup"><span data-stu-id="9d723-148">Enter **10.0.1.0/24** for **Address range**.</span></span>  <span data-ttu-id="9d723-149">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9d723-149">Click **OK**.</span></span>
8. <span data-ttu-id="9d723-150">En hello **myVnet - subredes** hoja, puede ver hello **público** y **privada** subredes que creó.</span><span class="sxs-lookup"><span data-stu-id="9d723-150">On hello **myVnet - Subnets** blade, you can see hello **Public** and **Private** subnets that you created.</span></span>
9. <span data-ttu-id="9d723-151">**Opcional**: al finalizar este tutorial, puede recursos de hello toodelete que ha creado, por lo que no se incurre en cargos por uso:</span><span class="sxs-lookup"><span data-stu-id="9d723-151">**Optional**: When you finish this tutorial, you might want toodelete hello resources that you created, so that you don't incur usage charges:</span></span>
    - <span data-ttu-id="9d723-152">Haga clic en **Introducción** en hello **myVnet** hoja.</span><span class="sxs-lookup"><span data-stu-id="9d723-152">Click **Overview** on hello **myVnet** blade.</span></span>
    - <span data-ttu-id="9d723-153">Haga clic en hello **eliminar** icono en hello **myVnet** hoja.</span><span class="sxs-lookup"><span data-stu-id="9d723-153">Click hello **Delete** icon on hello **myVnet** blade.</span></span>
    - <span data-ttu-id="9d723-154">eliminación de hello tooconfirm, haga clic en **Sí** en hello **red virtual de Delete** cuadro.</span><span class="sxs-lookup"><span data-stu-id="9d723-154">tooconfirm hello deletion, click **Yes** in hello **Delete virtual network** box.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="9d723-155">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="9d723-155">Azure CLI</span></span>

1. <span data-ttu-id="9d723-156">Puede seleccionar [instalar y configurar hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), o usar hello CLI en hello Shell en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="9d723-156">You can either [install and configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), or use hello CLI within hello Azure Cloud Shell.</span></span> <span data-ttu-id="9d723-157">Hola Shell en la nube de Azure es un shell de Bash gratuito que se puede ejecutar directamente dentro de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9d723-157">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="9d723-158">Tiene hello Azure CLI preinstalado y configurado toouse con su cuenta.</span><span class="sxs-lookup"><span data-stu-id="9d723-158">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="9d723-159">Ayuda de tooget para los comandos CLI, escriba `azure <command> --help`.</span><span class="sxs-lookup"><span data-stu-id="9d723-159">tooget help for CLI commands, type `azure <command> --help`.</span></span> 
2. <span data-ttu-id="9d723-160">En una sesión CLI, inicie sesión en tooAzure con el comando de Hola que sigue.</span><span class="sxs-lookup"><span data-stu-id="9d723-160">In a CLI session, log in tooAzure with hello command that follows.</span></span> <span data-ttu-id="9d723-161">Si hace clic en **Pruébelo** en el cuadro de Hola a continuación, se abre un Shell en la nube.</span><span class="sxs-lookup"><span data-stu-id="9d723-161">If you click **Try it** in hello box below, a Cloud Shell opens.</span></span> <span data-ttu-id="9d723-162">Puede iniciar sesión en tooyour suscripción de Azure, sin escribir Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="9d723-162">You can log in tooyour Azure subscription, without entering hello following command:</span></span>

    ```azurecli-interactive
    azure login
    ```

3. <span data-ttu-id="9d723-163">Hola tooensure CLI está en modo de administración de servicios, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="9d723-163">tooensure hello CLI is in Service Management mode, enter hello following command:</span></span>

    ```azurecli-interactive
    azure config mode asm
    ```

4. <span data-ttu-id="9d723-164">Cree una red virtual con una subred privada:</span><span class="sxs-lookup"><span data-stu-id="9d723-164">Create a virtual network with a private subnet:</span></span>

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. <span data-ttu-id="9d723-165">Crear una subred pública dentro de la red virtual de hello:</span><span class="sxs-lookup"><span data-stu-id="9d723-165">Create a public subnet within hello virtual network:</span></span>

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. <span data-ttu-id="9d723-166">Revisar la red virtual de Hola y subredes:</span><span class="sxs-lookup"><span data-stu-id="9d723-166">Review hello virtual network and subnets:</span></span>

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. <span data-ttu-id="9d723-167">**Opcional**: es recomendable recursos de hello toodelete que creó al finalizar este tutorial, por lo que no se incurre en cargos de uso:</span><span class="sxs-lookup"><span data-stu-id="9d723-167">**Optional**: You might want toodelete hello resources that you created when you finish this tutorial, so that you don't incur usage charges:</span></span>

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> <span data-ttu-id="9d723-168">Aunque no se puede especificar un toocreate de grupo de recursos una red virtual (clásica) en utilizando Hola CLI, Azure crea la red virtual de hello en un grupo de recursos denominado *redes predeterminado*.</span><span class="sxs-lookup"><span data-stu-id="9d723-168">Though you can't specify a resource group toocreate a virtual network (classic) in using hello CLI, Azure creates hello virtual network in a resource group named *Default-Networking*.</span></span>

## <a name="powershell"></a><span data-ttu-id="9d723-169">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d723-169">PowerShell</span></span>

1. <span data-ttu-id="9d723-170">Instale Hola la versión más reciente de hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) módulo.</span><span class="sxs-lookup"><span data-stu-id="9d723-170">Install hello latest version of hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) module.</span></span> <span data-ttu-id="9d723-171">Si está tooAzure nuevo PowerShell, consulte [Introducción a Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9d723-171">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="9d723-172">Inicie una sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9d723-172">Start a PowerShell session.</span></span>
3. <span data-ttu-id="9d723-173">En PowerShell, inicie sesión en tooAzure escribiendo hello `Add-AzureAccount` comando.</span><span class="sxs-lookup"><span data-stu-id="9d723-173">In PowerShell, log in tooAzure by entering hello `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="9d723-174">Cambiar Hola siguiente ruta de acceso y nombre de archivo, según corresponda, a continuación, exportación el archivo de configuración de red existente:</span><span class="sxs-lookup"><span data-stu-id="9d723-174">Change hello following path and filename, as appropriate, then export your existing network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. <span data-ttu-id="9d723-175">toocreate una red virtual con subredes privadas y públicas, use cualquier hello tooadd de editor de texto **VirtualNetworkSite** elemento que sigue toohello archivo de configuración de red.</span><span class="sxs-lookup"><span data-stu-id="9d723-175">toocreate a virtual network with public and private subnets, use any text editor tooadd hello **VirtualNetworkSite** element that follows toohello network configuration file.</span></span>

    ```xml
    <VirtualNetworkSite name="myVnet" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Private">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Public">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    ```

    <span data-ttu-id="9d723-176">Hola de revisión completa [esquema de archivo de configuración de red](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d723-176">Review hello full [network configuration file schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

6. <span data-ttu-id="9d723-177">Importar archivo de configuración de red de hello:</span><span class="sxs-lookup"><span data-stu-id="9d723-177">Import hello network configuration file:</span></span>

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > <span data-ttu-id="9d723-178">Importar un archivo de configuración de red modificado puede provocar cambios tooexisting redes virtuales (clásicas) en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="9d723-178">Importing a changed network configuration file can cause changes tooexisting virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="9d723-179">Asegúrese de sólo agregar red virtual anterior de Hola y que no cambiar o quitar cualquier red virtual existente de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="9d723-179">Ensure you only add hello previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 

7. <span data-ttu-id="9d723-180">Revisar la red virtual de Hola y subredes:</span><span class="sxs-lookup"><span data-stu-id="9d723-180">Review hello virtual network and subnets:</span></span>

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. <span data-ttu-id="9d723-181">**Opcional**: es recomendable recursos de hello toodelete que creó al finalizar este tutorial, por lo que no se incurre en cargos por uso.</span><span class="sxs-lookup"><span data-stu-id="9d723-181">**Optional**: You might want toodelete hello resources that you created when you finish this tutorial, so that you don't incur usage charges.</span></span> <span data-ttu-id="9d723-182">red virtual de Hola de toodelete, completar pasos 4 a 6 de nuevo, este Hola quitar tiempo **VirtualNetworkSite** elemento agregado en el paso 5.</span><span class="sxs-lookup"><span data-stu-id="9d723-182">toodelete hello virtual network, complete steps 4-6 again, this time removing hello **VirtualNetworkSite** element you added in step 5.</span></span>
 
> [!NOTE]
> <span data-ttu-id="9d723-183">Aunque no se puede especificar un toocreate de grupo de recursos una red virtual (clásica) en uso de PowerShell, Azure crea la red virtual de hello en un grupo de recursos denominado *redes predeterminado*.</span><span class="sxs-lookup"><span data-stu-id="9d723-183">Though you can't specify a resource group toocreate a virtual network (classic) in using PowerShell, Azure creates hello virtual network in a resource group named *Default-Networking*.</span></span>

---

## <a name="next-steps"></a><span data-ttu-id="9d723-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9d723-184">Next steps</span></span>

- <span data-ttu-id="9d723-185">toolearn sobre todo red virtual y la configuración de subred, consulte [administrar redes virtuales](virtual-network-manage-network.md) y [administrar subredes de red virtual](virtual-network-manage-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="9d723-185">toolearn about all virtual network and subnet settings, see [Manage virtual networks](virtual-network-manage-network.md) and [Manage virtual network subnets](virtual-network-manage-subnet.md).</span></span> <span data-ttu-id="9d723-186">Tienes varias opciones para el uso de redes virtuales y subredes en un requisitos diferentes toomeet del entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9d723-186">You have various options for using virtual networks and subnets in a production environment toomeet different requirements.</span></span>
- <span data-ttu-id="9d723-187">toofilter entrante y saliente el tráfico de subred, crear y aplicar [grupos de seguridad de red](virtual-networks-nsg.md) toosubnets.</span><span class="sxs-lookup"><span data-stu-id="9d723-187">toofilter inbound and outbound subnet traffic, create and apply [network security groups](virtual-networks-nsg.md) toosubnets.</span></span>
- <span data-ttu-id="9d723-188">Crear un [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o un [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) máquina virtual y, a continuación, conéctelo tooan de red virtual existente.</span><span class="sxs-lookup"><span data-stu-id="9d723-188">Create a [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or a [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtual machine, and then connect it tooan existing virtual network.</span></span>
- <span data-ttu-id="9d723-189">las redes virtuales tooconnect dos en Hola la misma ubicación de Azure, cree un [intercambio de tráfico de red virtual](create-peering-different-deployment-models.md) entre redes virtuales Hola.</span><span class="sxs-lookup"><span data-stu-id="9d723-189">tooconnect two virtual networks in hello same Azure location, create a  [virtual network peering](create-peering-different-deployment-models.md) between hello virtual networks.</span></span> <span data-ttu-id="9d723-190">Puede del mismo nivel de una red virtual (clásica) tooa de red virtual (Administrador de recursos), pero no se puede crear un emparejamiento entre dos redes virtuales (clásicas).</span><span class="sxs-lookup"><span data-stu-id="9d723-190">You can peer a virtual network (Resource Manager) tooa virtual network (classic), but you cannot create a peering between two virtual networks (classic).</span></span>
- <span data-ttu-id="9d723-191">Conectar hello tooan local red virtual mediante un [puerta de enlace VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o [ExpressRoute de Azure](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuito.</span><span class="sxs-lookup"><span data-stu-id="9d723-191">Connect hello virtual network tooan on-premises network by using a [VPN Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.</span></span>
