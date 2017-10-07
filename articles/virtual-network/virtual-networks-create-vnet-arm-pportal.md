---
title: una red virtual de Azure con varias subredes aaaCreate | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una red virtual con varias subredes en Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ad679a4-a959-4e48-a317-d9f5655a442b
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 0f56fa6ac24537d33b8e217f5b03f387826ab487
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-multiple-subnets"></a>Creación de una red virtual con varias subredes

En este tutorial, obtenga información acerca de cómo toocreate una red virtual Azure básica que tenga separar subredes públicas y privadas. Puede crear recursos de Azure, como máquinas virtuales, entornos de App Service, conjuntos de escalado de máquinas virtuales, Azure HDInsight y servicios en la nube en una subred. Recursos en redes virtuales puedan comunicarse entre sí y con los recursos de otra red virtual conectado tooa de redes.

Hello las secciones siguientes incluyen los pasos que debe seguir toocreate una red virtual mediante el uso de hello [portal de Azure](#portal), Hola interfaz de línea de comandos de Azure ([CLI de Azure](#azure-cli)), [PowerShell de Azure ](#powershell)y un [plantilla de Azure Resource Manager](#resource-manager-template). resultado de Hello es Hola mismo, independientemente de qué herramienta usar red virtual de toocreate Hola. Haga clic en una herramienta toogo toothat eslabones del tutorial Hola. Más información sobre todos los valores de [red virtual](virtual-network-manage-network.md) y [subred](virtual-network-manage-subnet.md).

Este artículo proporciona pasos toocreate una red virtual a través del modelo de implementación de administrador de recursos de hello, que es el modelo de implementación de Hola que se recomienda usar al crear nuevas redes virtuales. Si necesita toocreate una red virtual (clásica), consulte [crear una red virtual (clásica)](create-virtual-network-classic.md). Si no está familiarizado con los modelos de implementación de Azure, vea [Understand Azure deployment models (Descripción de los modelos de implementación de Azure)](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).

## <a name="portal"></a>Azure Portal

1. En un explorador de Internet, vaya toohello [portal de Azure](https://portal.azure.com). Inicie sesión con la [cuenta de Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Si no tiene una cuenta de Azure, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
2. En el portal de hello, haga clic en **+ nuevo** > **red** > **red Virtual**.
3. En hello **crear red virtual** hoja, escriba Hola después de valores y, a continuación, haga clic en **crear**:

    |Configuración|Valor|
    |---|---|
    |Nombre|myVnet|
    |Espacio de direcciones|10.0.0.0/16|
    |Nombre de subred|Público|
    |Intervalo de direcciones de subred|10.0.0.0/24|
    |Grupos de recursos|Deje seleccionado **Crear nuevo** y después escriba **myResourceGroup**.|
    |Suscripción y ubicación|Seleccione su suscripción y ubicación.

    Si es nuevo tooAzure, obtenga más información sobre [grupos de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [suscripciones](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), y [ubicaciones](https://azure.microsoft.com/regions) (también denominada tooas *regiones*).
4. En el portal de hello, puede crear solo una subred cuando se crea una red virtual. En este tutorial, creará una segunda subred después de crear la red virtual de Hola. Más adelante puede crear recursos accesibles desde Internet en hello **público** subred. También puede crear recursos que no son accesibles desde Internet de Hola Hola **privada** subred. toocreate Hola segunda subred, Hola **buscar recursos** cuadro al principio de Hola de página de hello, escriba **myVnet**. En los resultados de la búsqueda de hello, haga clic en **myVnet**. Si tiene varias redes virtuales con Hola el mismo nombre en su suscripción, compruebe los grupos de recursos de Hola que aparecen en cada red virtual. Asegúrese de que haga clic en hello **myVnet** buscar resultados que tiene el grupo de recursos de hello **myResourceGroup**.
5. En hello **myVnet** hoja, en **configuración**, haga clic en **subredes**.
6. En hello **myVnet - subredes** hoja, haga clic en **+ subred**.
7. En hello **Agregar subred** hoja, para **nombre**, escriba **privada**. Para **Intervalo de direcciones**, escriba **10.0.1.0/24**.  Haga clic en **Aceptar**.
8. En hello **myVnet - subredes** hoja, revisión Hola subredes. Puede ver hello **público** y **privada** subredes que creó.
9. **Opcional:** toodelete los recursos de Hola que creará en este tutorial, Hola completa los pasos de [eliminar recursos](#delete-portal) en este artículo.

## <a name="azure-cli"></a>CLI de Azure

Comandos de CLI de Azure son Hola iguales, ya que ejecutar comandos de Hola de Windows, Linux o Mac OS. Pero existen diferencias de scripting entre los shells del sistema operativo. script de Hola Hola siguiendo los pasos que se ejecuta en un shell de Bash. 

1. [Instalar y configurar hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Asegúrese de que tiene la versión más reciente de Hola de hello CLI de Azure instalado. Ayuda de tooget para los comandos CLI, escriba `az <command> --help`. En lugar de instalar Hola CLI y sus requisitos previos, puede usar Hola Shell en la nube de Azure. Hola Shell en la nube de Azure es un shell de Bash gratuito que se puede ejecutar directamente dentro de hello portal de Azure. Hola Shell en la nube tiene hello Azure CLI preinstalado y configurado toouse con su cuenta. Hola toouse Shell en la nube, haga clic en hello Shell en la nube (**> _**) situado en la parte superior de Hola de hello [portal](https://portal.azure.com) o simplemente haga clic en hello *Pruébelo* botón Hola siguientes pasos. 
2. Si ejecuta localmente Hola CLI, inicie sesión en tooAzure con hello `az login` comando. Si usa Hola Shell en la nube, ya inició sesión.
3. Hola de revisión después de la secuencia de comandos y sus comentarios. En el explorador, copie el script de Hola y péguelo en la sesión CLI:

    ```azurecli-interactive
    #!/bin/bash
    
    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus
    
    # Create a virtual network with one subnet named Public.
    az network vnet create \
      --name myVnet \
      --resource-group myResourceGroup \
      --subnet-name Public
    
    # Create an additional subnet named Private in hello virtual network.
    az network vnet subnet create \
      --name Private \
      --address-prefix 10.0.1.0/24 \
      --vnet-name myVnet \
      --resource-group myResourceGroup
    ```
    
4. Cuando finalice el script de Hola ejecutando, revise las subredes de hello para la red virtual de Hola. Copie el siguiente comando de hello y, a continuación, péguelo en la sesión CLI:

    ```azurecli
    az network vnet subnet list --resource-group myResourceGroup --vnet-name myVnet --output table
    ```

5. **Opcional**: recursos de hello toodelete que creará en este tutorial, Hola completa los pasos de [eliminar recursos](#delete-cli) en este artículo.

## <a name="powershell"></a>PowerShell

1. Instale Hola la versión más reciente de hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo. Si está tooAzure nuevo PowerShell, consulte [Introducción a Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. En una sesión de PowerShell, inicie sesión en tooAzure con su [cuenta de Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) con hello `login-azurermaccount` comando.

3. Hola de revisión después de la secuencia de comandos y sus comentarios. En el explorador, copie el script de Hola y péguelo en la sesión de PowerShell:

    ```powershell
    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name myResourceGroup `
      -Location eastus
    
    # Create hello public and private subnets.
    $Subnet1 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Public `
      -AddressPrefix 10.0.0.0/24
    $Subnet2 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Private `
      -AddressPrefix 10.0.1.0/24
    
    # Create a virtual network.
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Location eastus `
      -Name myVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet1,$Subnet2
    ```

4. subredes de hello tooreview para la red virtual de hello, copie el siguiente comando de hello y, a continuación, péguelo en la sesión de PowerShell:

    ```powershell
    $Vnet.subnets | Format-Table Name, AddressPrefix
    ```

5. **Opcional**: recursos de hello toodelete que creará en este tutorial, Hola completa los pasos de [eliminar recursos](#delete-powershell) en este artículo.

## <a name="resource-manager-template"></a>Plantilla de Resource Manager

Puede implementar una red virtual con una plantilla de Azure Resource Manager. toolearn más información sobre plantillas, consulte [¿qué es el Administrador de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#template-deployment). plantilla de hello tooaccess y toolearn acerca de sus parámetros, vea hello [crear una red virtual con dos subredes](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) plantilla. Puede implementar la plantilla de hello mediante hello [portal](#template-portal), [CLI de Azure](#template-cli), o [PowerShell](#template-powershell).

**Opcional:** toodelete los recursos de Hola que creará en este tutorial, Hola completa los pasos en las subsecciones de [eliminar recursos](#delete) en este artículo.

### <a name="template-portal"></a>Azure Portal

1. En el explorador, abra hello [página de la plantilla](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets).
2. Haga clic en hello **implementar tooAzure** botón. Si aún no ha iniciado sesión en tooAzure, inicie sesión en la pantalla de inicio de sesión de portal Azure de bienvenida que aparece.
3. Inicie sesión en el portal de toohello mediante su [cuenta de Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Si no tiene una cuenta de Azure, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
4. Escriba Hola después de valores para parámetros de hello:

    |Parámetro|Valor|
    |---|---|
    |Subscription|Seleccione su suscripción.|
    |Grupos de recursos|myResourceGroup|
    |Ubicación|Seleccionar una ubicación|
    |Nombre de red virtual|myVnet|
    |Prefijo de dirección de la red virtual|10.0.0.0/16|
    |Subnet1Prefix|10.0.0.0/24|
    |Subnet1Name|Público|
    |Subnet2Prefix|10.0.1.0/24|
    |Subnet2Name|Privada|

5. Acepta toohello términos y condiciones y, a continuación, haga clic en **compra** red virtual de toodeploy Hola.

### <a name="template-cli"></a>Azure CLI

1. [Instalar y configurar hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Asegúrese de que tiene la versión más reciente de Hola de hello CLI de Azure instalado. Ayuda de tooget para los comandos CLI, escriba `az <command> --help`. En lugar de instalar Hola CLI y sus requisitos previos, puede usar Hola Shell en la nube de Azure. Hola Shell en la nube de Azure es un shell de Bash gratuito que se puede ejecutar directamente dentro de hello portal de Azure. Hola Shell en la nube tiene hello Azure CLI preinstalado y configurado toouse con su cuenta. Hola toouse Shell en la nube, haga clic en hello Shell en la nube **> _** situado en la parte superior de Hola de hello [portal](https://portal.azure.com), o simplemente haga clic en hello **Pruébelo** botón Hola siguientes pasos. 
2. Si ejecuta localmente Hola CLI, inicie sesión en tooAzure con hello `az login` comando. Si usa Hola Shell en la nube, ya inició sesión.
3. toocreate un grupo de recursos de red virtual de hello, comando copia Hola siguiente y péguelo en la sesión CLI:

    ```azurecli-interactive
    az group create --name myResourceGroup --location eastus
    ```
    
4. Puede implementar la plantilla de hello mediante una de las siguientes opciones de parámetros de Hola:
    - **Valores de parámetro predeterminados**. Escriba el siguiente comando de hello:
    
        ```azurecli-interactive
        az group deployment create --resource-group myResourceGroup --name VnetTutorial --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json`
        ```
    - **Valores de parámetro personalizados**. Descargar y modificar la plantilla de hello antes de implementar la plantilla de Hola. También puede implementar la plantilla de hello mediante el uso de parámetros en la línea de comandos de Hola o implementar la plantilla de hello con un archivo de parámetros separados. archivos de plantilla y los parámetros de hello toodownload, haga clic en hello **examinar en GitHub** botón en hello [crear una red virtual con dos subredes](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) página de la plantilla. En GitHub, haga clic en hello **azuredeploy.parameters.json** o **azuredeploy.json** archivo. A continuación, haga clic en hello **Raw** archivo de hello toodisplay de botón. En el explorador, copie el contenido de Hola de archivo hello. Guardar archivo de tooa de contenido de hello en el equipo. Puede modificar los valores de parámetro de hello en la plantilla de Hola o implementar la plantilla de hello con un archivo de parámetros separados.  

    toolearn Obtenga más información sobre cómo toodeploy plantillas mediante el uso de estos métodos, escriba `az group deployment create --help`.

### <a name="template-powershell"></a>PowerShell

1. Instale Hola la versión más reciente de hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo. Si está tooAzure nuevo PowerShell, consulte [Introducción a Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. En una sesión de PowerShell, toosign sesión con su [cuenta de Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account), escriba `login-azurermaccount`.
3. toocreate un grupo de recursos de red virtual de hello, escriba Hola siguiente comando:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
    ```
    
4. Puede implementar la plantilla de hello mediante una de las siguientes opciones de parámetros de Hola:
    - **Valores de parámetro predeterminados**. Escriba el siguiente comando de hello:
    
        ```powershell
        New-AzureRmResourceGroupDeployment -Name VnetTutorial -ResourceGroupName myResourceGroup -TemplateUri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json
        ```
        
    - **Valores de parámetro personalizados**. Descargar y modificar la plantilla de hello antes de implementarlo. También puede implementar la plantilla de hello mediante el uso de parámetros en la línea de comandos de Hola o implementar la plantilla de hello con un archivo de parámetros separados. archivos de plantilla y los parámetros de hello toodownload, haga clic en hello **examinar en GitHub** botón en hello [crear una red virtual con dos subredes](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) página de la plantilla. En GitHub, haga clic en hello **azuredeploy.parameters.json** o **azuredeploy.json** archivo. A continuación, haga clic en hello **Raw** archivo de hello toodisplay de botón. En el explorador, copie el contenido de Hola de archivo hello. Guardar archivo de tooa de contenido de hello en el equipo. Puede modificar los valores de parámetro de hello en la plantilla de Hola o implementar la plantilla de hello con un archivo de parámetros separados.  

    toolearn Obtenga más información sobre cómo toodeploy plantillas mediante el uso de estos métodos, escriba `Get-Help New-AzureRmResourceGroupDeployment`. 

## <a name="delete"></a>Eliminación de recursos

Cuando haya terminado este tutorial, conviene recursos de hello toodelete que ha creado, por lo que no se incurre en cargos por uso. Eliminación de un grupo de recursos, también elimina todos los recursos que se encuentran en el grupo de recursos de Hola.

### <a name="delete-portal"></a>Azure Portal

1. En el cuadro de búsqueda del portal de hello, escriba **myResourceGroup**. En los resultados de la búsqueda de hello, haga clic en **myResourceGroup**.
2. En hello **myResourceGroup** hoja, haga clic en hello **eliminar** icono.
3. eliminación de hello tooconfirm, Hola **Hola nombre del grupo de recursos de tipo** cuadro, escriba **myResourceGroup**y, a continuación, haga clic en **eliminar**.

### <a name="delete-cli"></a>Azure CLI

En una sesión CLI, escriba Hola siguiente comando:

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <a name="delete-powershell"></a>PowerShell

En una sesión de PowerShell, escriba Hola siguiente comando:

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="next-steps"></a>Pasos siguientes

- toolearn sobre todo red virtual y la configuración de subred, consulte [administrar redes virtuales](virtual-network-manage-network.md#view-vnet) y [administrar subredes de red virtual](virtual-network-manage-subnet.md#create-subnet). Tienes varias opciones para el uso de redes virtuales y subredes en un requisitos diferentes toomeet del entorno de producción.
- toofilter entrante y saliente el tráfico de subred, crear y aplicar [grupos de seguridad de red](virtual-networks-nsg.md) toosubnets.
- Crear un [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o un [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) máquina virtual y, a continuación, conéctelo tooan de red virtual existente.
- las redes virtuales tooconnect dos en Hola la misma ubicación de Azure, cree un [intercambio de tráfico de red virtual](virtual-network-peering-overview.md) entre redes virtuales Hola.
- Conectar hello tooan local red virtual mediante un [puerta de enlace VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o [ExpressRoute de Azure](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuito.
