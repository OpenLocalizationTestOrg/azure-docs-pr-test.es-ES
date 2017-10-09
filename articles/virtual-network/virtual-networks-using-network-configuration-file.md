---
title: "una red Virtual de Azure (clásico): archivo de configuración de red aaaConfigure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate y modificar redes virtuales (clásicas) exportar, cambiar e importando un archivo de configuración de red."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c29b9059-22b0-444e-bbfe-3e35f83cde2f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 009108d4315b4b7146d3f1cf2436ee211d2d89ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a><span data-ttu-id="ed65a-103">Configuración de una red virtual (clásica) mediante un archivo de configuración de red</span><span class="sxs-lookup"><span data-stu-id="ed65a-103">Configure a virtual network (classic) using a network configuration file</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ed65a-104">Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [el Administrador de recursos y el clásico](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ed65a-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="ed65a-105">Este artículo incluye el uso de modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed65a-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="ed65a-106">Microsoft recomienda que más nuevas implementaciones utilizarán modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed65a-106">Microsoft recommends that most new deployments use hello Resource Manager deployment model.</span></span>

<span data-ttu-id="ed65a-107">Puede crear y configurar una red virtual (clásica) con un archivo de configuración de red mediante hello Azure interfaz de línea de comandos (CLI) 1.0 o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed65a-107">You can create and configure a virtual network (classic) with a network configuration file using hello Azure command-line interface (CLI) 1.0 or Azure PowerShell.</span></span> <span data-ttu-id="ed65a-108">No se puede crear o modificar una red virtual a través del modelo de implementación de Azure Resource Manager Hola con un archivo de configuración de red.</span><span class="sxs-lookup"><span data-stu-id="ed65a-108">You cannot create or modify a virtual network through hello Azure Resource Manager deployment model using a network configuration file.</span></span> <span data-ttu-id="ed65a-109">No se puede usar hello Azure toocreate portal o modificar una red virtual (clásica) con un archivo de configuración de red, pero puede usar Hola toocreate portal Azure una red virtual (clásica), sin utilizar un archivo de configuración de red.</span><span class="sxs-lookup"><span data-stu-id="ed65a-109">You cannot use hello Azure portal toocreate or modify a virtual network (classic) using a network configuration file, however you can use hello Azure portal toocreate a virtual network (classic), without using a network configuration file.</span></span>

<span data-ttu-id="ed65a-110">Crear y configurar una red virtual (clásica) con un archivo de configuración de red requieren exportar, cambiar e importar archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed65a-110">Creating and configuring a virtual network (classic) with a network configuration file requires exporting, changing, and importing hello file.</span></span>

## <span data-ttu-id="ed65a-111"><a name="export"></a>Exportación de un archivo de configuración de red</span><span class="sxs-lookup"><span data-stu-id="ed65a-111"><a name="export"></a>Export a network configuration file</span></span>

<span data-ttu-id="ed65a-112">También puede usar PowerShell o hello Azure CLI tooexport un archivo de configuración de red.</span><span class="sxs-lookup"><span data-stu-id="ed65a-112">You can use PowerShell or hello Azure CLI tooexport a network configuration file.</span></span> <span data-ttu-id="ed65a-113">PowerShell exporta un archivo XML, mientras que hello Azure CLI exporta un archivo json.</span><span class="sxs-lookup"><span data-stu-id="ed65a-113">PowerShell exports an XML file, while hello Azure CLI exports a json file.</span></span>

### <a name="powershell"></a><span data-ttu-id="ed65a-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed65a-114">PowerShell</span></span>
 
1. <span data-ttu-id="ed65a-115">[Instale Azure PowerShell e inicie sesión en tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ed65a-115">[Install Azure PowerShell and sign in tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="ed65a-116">Cambie el directorio de hello (y asegurarse de que exista) y nombre de archivo en hello siguiente comando como deseado y luego ejecución Hola comando tooexport Hola del archivo de configuración:</span><span class="sxs-lookup"><span data-stu-id="ed65a-116">Change hello directory (and ensure it exists) and filename in hello following command as desired, then run hello command tooexport hello network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="ed65a-117">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="ed65a-117">Azure CLI 1.0</span></span>

1. <span data-ttu-id="ed65a-118">[Instalar hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ed65a-118">[Install hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="ed65a-119">Completar Hola restantes pasos desde un símbolo del sistema de Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="ed65a-119">Complete hello remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="ed65a-120">Inicie sesión en tooAzure escribiendo hello `azure login` comando.</span><span class="sxs-lookup"><span data-stu-id="ed65a-120">Log in tooAzure by entering hello `azure login` command.</span></span>
3. <span data-ttu-id="ed65a-121">Asegúrese de que está en modo de asm escribiendo hello `azure config mode asm` comando.</span><span class="sxs-lookup"><span data-stu-id="ed65a-121">Ensure you're in asm mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="ed65a-122">Cambie el directorio de hello (y asegurarse de que exista) y nombre de archivo en hello siguiente comando como deseado y luego ejecución Hola comando tooexport Hola del archivo de configuración:</span><span class="sxs-lookup"><span data-stu-id="ed65a-122">Change hello directory (and ensure it exists) and filename in hello following command as desired, then run hello command tooexport hello network configuration file:</span></span>
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a><span data-ttu-id="ed65a-123">Creación o modificación mediante el archivo de configuración de red</span><span class="sxs-lookup"><span data-stu-id="ed65a-123">Create or modify a network configuration file</span></span>

<span data-ttu-id="ed65a-124">Un archivo de configuración de red es un archivo XML (cuando se usa PowerShell) o un archivo json (cuando se usa Hola CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="ed65a-124">A network configuration file is an XML file (when using PowerShell) or a json file (when using hello Azure CLI).</span></span> <span data-ttu-id="ed65a-125">Puede editar el archivo hello en cualquier texto o editor XML/json.</span><span class="sxs-lookup"><span data-stu-id="ed65a-125">You can edit hello file in any text, or XML/json editor.</span></span> <span data-ttu-id="ed65a-126">Hola [opciones de esquema de archivo de configuración de red](https://msdn.microsoft.com/library/azure/jj157100.aspx) artículo incluye los detalles de todas las configuraciones.</span><span class="sxs-lookup"><span data-stu-id="ed65a-126">hello [Network configuration file schema settings](https://msdn.microsoft.com/library/azure/jj157100.aspx) article includes details for all settings.</span></span> <span data-ttu-id="ed65a-127">Para una explicación adicional de valores de hello, consulte [ver redes virtuales y la configuración](virtual-network-manage-network.md#view-vnet).</span><span class="sxs-lookup"><span data-stu-id="ed65a-127">For additional explanation of hello settings, see [View virtual networks and settings](virtual-network-manage-network.md#view-vnet).</span></span> <span data-ttu-id="ed65a-128">cambios de Hola que realice toohello archivo:</span><span class="sxs-lookup"><span data-stu-id="ed65a-128">hello changes you make toohello file:</span></span>

- <span data-ttu-id="ed65a-129">Debe ser compatible con el esquema de Hola o importación de Hola de red, archivo de configuración se producirá un error.</span><span class="sxs-lookup"><span data-stu-id="ed65a-129">Must comply with hello schema, or importing hello network configuration file will fail.</span></span>
- <span data-ttu-id="ed65a-130">Sobrescriben cualquier configuración de red existente para su suscripción, por lo que debe tener mucho cuidado al realizar modificaciones.</span><span class="sxs-lookup"><span data-stu-id="ed65a-130">Overwrite any existing network settings for your subscription, so use extreme caution when making modifications.</span></span> <span data-ttu-id="ed65a-131">Por ejemplo, hacer referencia a archivos de configuración de red de ejemplo de Hola que siguen.</span><span class="sxs-lookup"><span data-stu-id="ed65a-131">For example, reference hello example network configuration files that follow.</span></span> <span data-ttu-id="ed65a-132">Indicar el archivo original de hello contiene dos **VirtualNetworkSite** instancias y se cambia, tal y como se muestra en los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="ed65a-132">Say hello original file contained two **VirtualNetworkSite** instances, and you changed it, as shown in hello examples.</span></span> <span data-ttu-id="ed65a-133">Cuando se importa el archivo hello, Azure elimina la red virtual de Hola para hello **VirtualNetworkSite** instancia quitó en el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="ed65a-133">When you import hello file, Azure deletes hello virtual network for hello **VirtualNetworkSite** instance you removed in hello file.</span></span> <span data-ttu-id="ed65a-134">Este escenario simplificado se da por supuesto que no hay recursos estaban en la red virtual de hello, como si hubiera, no se pudo eliminar la red virtual de Hola y se producirá un error en la importación de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed65a-134">This simplified scenario assumes no resources were in hello virtual network, as if there were, hello virtual network could not be deleted, and hello import would fail.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ed65a-135">Azure considera que una subred que tiene algo implementado tooit como **en uso**.</span><span class="sxs-lookup"><span data-stu-id="ed65a-135">Azure considers a subnet that has something deployed tooit as **in use**.</span></span> <span data-ttu-id="ed65a-136">Cuando una subred está en uso, no puede modificarse.</span><span class="sxs-lookup"><span data-stu-id="ed65a-136">When a subnet is in use, it cannot be modified.</span></span> <span data-ttu-id="ed65a-137">Antes de modificar la información de subred en un archivo de configuración de red, mueva todo lo que ha implementado toohello subred tooa otra subred que no se esté modificando.</span><span class="sxs-lookup"><span data-stu-id="ed65a-137">Before modifying subnet information in a network configuration file, move anything that you have deployed toohello subnet tooa different subnet that isn't being modified.</span></span> <span data-ttu-id="ed65a-138">Vea [mover una máquina virtual o instancia de rol tooa otra subred](virtual-networks-move-vm-role-to-subnet.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="ed65a-138">See [Move a VM or Role Instance tooa Different Subnet](virtual-networks-move-vm-role-to-subnet.md) for details.</span></span>

### <a name="example-xml-for-use-with-powershell"></a><span data-ttu-id="ed65a-139">XML de ejemplo para su uso con PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed65a-139">Example XML for use with PowerShell</span></span>

<span data-ttu-id="ed65a-140">Hello siguiente archivo de configuración de red en el ejemplo crea una red virtual denominada *myVirtualNetwork* con un espacio de direcciones de *10.0.0.0/16* en hello *UU* Azure región.</span><span class="sxs-lookup"><span data-stu-id="ed65a-140">hello following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in hello *East US* Azure region.</span></span> <span data-ttu-id="ed65a-141">una subred con el nombre de red virtual de Hello contiene *mySubnet* con un prefijo de dirección de *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="ed65a-141">hello virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
  <VirtualNetworkConfiguration>
    <Dns />
    <VirtualNetworkSites>
      <VirtualNetworkSite name="myVirtualNetwork" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="mySubnet">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>
  </VirtualNetworkConfiguration>
</NetworkConfiguration>
```

<span data-ttu-id="ed65a-142">Si Hola del archivo de configuración exportado no contiene ningún contenido, puede copiar Hola XML en el ejemplo anterior de Hola y péguelo en un nuevo archivo.</span><span class="sxs-lookup"><span data-stu-id="ed65a-142">If hello network configuration file you exported contains no contents, you can copy hello XML in hello previous example, and paste it into a new file.</span></span>

### <a name="example-json-for-use-with-hello-azure-cli-10"></a><span data-ttu-id="ed65a-143">JSON de ejemplo para su uso con hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="ed65a-143">Example JSON for use with hello Azure CLI 1.0</span></span>

<span data-ttu-id="ed65a-144">Hello siguiente archivo de configuración de red en el ejemplo crea una red virtual denominada *myVirtualNetwork* con un espacio de direcciones de *10.0.0.0/16* en hello *UU* Azure región.</span><span class="sxs-lookup"><span data-stu-id="ed65a-144">hello following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in hello *East US* Azure region.</span></span> <span data-ttu-id="ed65a-145">una subred con el nombre de red virtual de Hello contiene *mySubnet* con un prefijo de dirección de *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="ed65a-145">hello virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

```json
{
   "VirtualNetworkConfiguration" : {
      "Dns" : "",
      "VirtualNetworkSites" : [
         {
            "AddressSpace" : [ "10.0.0.0/16" ],
            "Location" : "East US",
            "Name" : "myVirtualNetwork",
            "Subnets" : [
               {
                  "AddressPrefix" : "10.0.0.0/24",
                  "Name" : "mySubnet"
               }
            ]
         }
      ]
   }
}
```

<span data-ttu-id="ed65a-146">Si Hola del archivo de configuración exportado no contiene ningún contenido, puede copiar json hello en el ejemplo anterior de Hola y péguelo en un nuevo archivo.</span><span class="sxs-lookup"><span data-stu-id="ed65a-146">If hello network configuration file you exported contains no contents, you can copy hello json in hello previous example, and paste it into a new file.</span></span>

## <span data-ttu-id="ed65a-147"><a name="import"></a>Importación de un archivo de configuración de red</span><span class="sxs-lookup"><span data-stu-id="ed65a-147"><a name="import"></a>Import a network configuration file</span></span>

<span data-ttu-id="ed65a-148">También puede usar PowerShell o hello Azure CLI tooimport un archivo de configuración de red.</span><span class="sxs-lookup"><span data-stu-id="ed65a-148">You can use PowerShell or hello Azure CLI tooimport a network configuration file.</span></span> <span data-ttu-id="ed65a-149">PowerShell importa un archivo XML, mientras que hello Azure CLI importa un archivo json.</span><span class="sxs-lookup"><span data-stu-id="ed65a-149">PowerShell imports an XML file, while hello Azure CLI imports a json file.</span></span> <span data-ttu-id="ed65a-150">Si se produce un error en la importación de hello, confirme ese archivo hello es compatible con hello [esquema de configuración de red](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="ed65a-150">If hello import fails, confirm that hello file complies with hello [network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span> 

### <a name="powershell"></a><span data-ttu-id="ed65a-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed65a-151">PowerShell</span></span>
 
1. <span data-ttu-id="ed65a-152">[Instale Azure PowerShell e inicie sesión en tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ed65a-152">[Install Azure PowerShell and sign in tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="ed65a-153">Cambiar el directorio de Hola y nombre de archivo en hello siguiente comando según sea necesario y luego ejecute el archivo de configuración de red de Hola Hola comando tooimport:</span><span class="sxs-lookup"><span data-stu-id="ed65a-153">Change hello directory and filename in hello following command as necessary, then run hello command tooimport hello network configuration file:</span></span>
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="ed65a-154">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="ed65a-154">Azure CLI 1.0</span></span>

1. <span data-ttu-id="ed65a-155">[Instalar hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ed65a-155">[Install hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="ed65a-156">Completar Hola restantes pasos desde un símbolo del sistema de Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="ed65a-156">Complete hello remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="ed65a-157">Inicie sesión en tooAzure escribiendo hello `azure login` comando.</span><span class="sxs-lookup"><span data-stu-id="ed65a-157">Log in tooAzure by entering hello `azure login` command.</span></span>
3. <span data-ttu-id="ed65a-158">Asegúrese de que está en modo de asm escribiendo hello `azure config mode asm` comando.</span><span class="sxs-lookup"><span data-stu-id="ed65a-158">Ensure you're in asm mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="ed65a-159">Cambiar el directorio de Hola y nombre de archivo en hello siguiente comando según sea necesario y luego ejecute el archivo de configuración de red de Hola Hola comando tooimport:</span><span class="sxs-lookup"><span data-stu-id="ed65a-159">Change hello directory and filename in hello following command as necessary, then run hello command tooimport hello network configuration file:</span></span>

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
