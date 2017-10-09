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
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a>Creación de una red virtual (clásica) con varias subredes

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Este artículo incluye el uso de modelo de implementación clásica de Hola. Microsoft recomienda crear mayoría nuevas redes virtuales a través de hello [el Administrador de recursos](virtual-networks-create-vnet-arm-pportal.md) modelo de implementación.

En este tutorial, obtenga información acerca de cómo toocreate una básica red virtual de Azure (clásica) que tiene separar subredes públicas y privadas. Puede crear recursos de Azure, como máquinas virtuales y servicios en la nube en una subred. Recursos creados en redes virtuales (clásicas) pueden comunicarse entre sí y con los recursos de otra red virtual conectado tooa de redes.

Más información sobre todos los valores de [red virtual](virtual-network-manage-network.md) y [subred](virtual-network-manage-subnet.md).

> [!WARNING]
> Azure elimina inmediatamente las redes virtuales (clásicas) cuando se [deshabilita una suscripción](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit). Redes virtuales (clásicas) se eliminan independientemente de que existan los recursos de red virtual de Hola. Si más adelante vuelve a habilitar suscripción hello, se deben recrear los recursos que existían en la red virtual de Hola.

Puede crear una red virtual (clásica) mediante hello [portal de Azure](#portal), hello [Azure interfaz de línea de comandos (CLI) 1.0](#azure-cli), o [PowerShell](#powershell).

## <a name="portal"></a>Portal

1. En un explorador de Internet, vaya toohello [portal de Azure](https://portal.azure.com). Inicie sesión con la [cuenta de Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Si no tiene una cuenta de Azure, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Haga clic en **+ nuevo** en el portal de Hola.
3. Escriba *red Virtual* en hello **Hola búsqueda Marketplace** cuadro principio de Hola de hello **New** hoja que aparece.  Haga clic en **red Virtual** cuando aparece en los resultados de búsqueda de Hola.
4. Seleccione **clásico** en hello **seleccionar un modelo de implementación** cuadro hello **red Virtual** hoja que aparece, haga clic en **crear**. 
5. Escriba Hola siguiente valores de hello **crear red virtual (clásica)** hoja y, a continuación, haga clic en **crear**:

    |Configuración|Valor|
    |---|---|
    |Nombre|myVnet|
    |Espacio de direcciones|10.0.0.0/16|
    |Nombre de subred|Público|
    |Intervalo de direcciones de subred|10.0.0.0/24|
    |Grupos de recursos|Deje seleccionado **Crear nuevo** y después escriba **myResourceGroup**.|
    |Suscripción y ubicación|Seleccione su suscripción y ubicación.

    Si es nuevo tooAzure, obtenga más información sobre [grupos de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [suscripciones](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), y [ubicaciones](https://azure.microsoft.com/regions) (también denominada tooas *regiones*).
4. En el portal de hello, puede crear solo una subred cuando se crea una red virtual. En este tutorial, creará una segunda subred después de crear la red virtual de Hola. Más adelante puede crear recursos accesibles desde Internet en hello **público** subred. También puede crear recursos que no son accesibles desde Internet de Hola Hola **privada** subred. toocreate Hola segunda subred, escriba **myVnet** en hello **buscar recursos** cuadro Hola principio de página Hola. Haga clic en **myVnet** cuando aparece en los resultados de búsqueda de Hola.
5. Haga clic en **subredes** (Hola **configuración** sección) en hello **crear red virtual (clásica)** hoja que aparece.
6. Haga clic en **+ agregar** en hello **myVnet - subredes** hoja que aparece.
7. Escriba **privada** para **nombre** en hello **Agregar subred** hoja. Especifique **10.0.1.0/24** para **Intervalo de direcciones**.  Haga clic en **Aceptar**.
8. En hello **myVnet - subredes** hoja, puede ver hello **público** y **privada** subredes que creó.
9. **Opcional**: al finalizar este tutorial, puede recursos de hello toodelete que ha creado, por lo que no se incurre en cargos por uso:
    - Haga clic en **Introducción** en hello **myVnet** hoja.
    - Haga clic en hello **eliminar** icono en hello **myVnet** hoja.
    - eliminación de hello tooconfirm, haga clic en **Sí** en hello **red virtual de Delete** cuadro.

## <a name="azure-cli"></a>CLI de Azure

1. Puede seleccionar [instalar y configurar hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), o usar hello CLI en hello Shell en la nube de Azure. Hola Shell en la nube de Azure es un shell de Bash gratuito que se puede ejecutar directamente dentro de hello portal de Azure. Tiene hello Azure CLI preinstalado y configurado toouse con su cuenta. Ayuda de tooget para los comandos CLI, escriba `azure <command> --help`. 
2. En una sesión CLI, inicie sesión en tooAzure con el comando de Hola que sigue. Si hace clic en **Pruébelo** en el cuadro de Hola a continuación, se abre un Shell en la nube. Puede iniciar sesión en tooyour suscripción de Azure, sin escribir Hola siguiente comando:

    ```azurecli-interactive
    azure login
    ```

3. Hola tooensure CLI está en modo de administración de servicios, escriba Hola siguiente comando:

    ```azurecli-interactive
    azure config mode asm
    ```

4. Cree una red virtual con una subred privada:

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. Crear una subred pública dentro de la red virtual de hello:

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. Revisar la red virtual de Hola y subredes:

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. **Opcional**: es recomendable recursos de hello toodelete que creó al finalizar este tutorial, por lo que no se incurre en cargos de uso:

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> Aunque no se puede especificar un toocreate de grupo de recursos una red virtual (clásica) en utilizando Hola CLI, Azure crea la red virtual de hello en un grupo de recursos denominado *redes predeterminado*.

## <a name="powershell"></a>PowerShell

1. Instale Hola la versión más reciente de hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) módulo. Si está tooAzure nuevo PowerShell, consulte [Introducción a Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Inicie una sesión de PowerShell.
3. En PowerShell, inicie sesión en tooAzure escribiendo hello `Add-AzureAccount` comando.
4. Cambiar Hola siguiente ruta de acceso y nombre de archivo, según corresponda, a continuación, exportación el archivo de configuración de red existente:

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. toocreate una red virtual con subredes privadas y públicas, use cualquier hello tooadd de editor de texto **VirtualNetworkSite** elemento que sigue toohello archivo de configuración de red.

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

    Hola de revisión completa [esquema de archivo de configuración de red](https://msdn.microsoft.com/library/azure/jj157100.aspx).

6. Importar archivo de configuración de red de hello:

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > Importar un archivo de configuración de red modificado puede provocar cambios tooexisting redes virtuales (clásicas) en su suscripción. Asegúrese de sólo agregar red virtual anterior de Hola y que no cambiar o quitar cualquier red virtual existente de su suscripción. 

7. Revisar la red virtual de Hola y subredes:

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. **Opcional**: es recomendable recursos de hello toodelete que creó al finalizar este tutorial, por lo que no se incurre en cargos por uso. red virtual de Hola de toodelete, completar pasos 4 a 6 de nuevo, este Hola quitar tiempo **VirtualNetworkSite** elemento agregado en el paso 5.
 
> [!NOTE]
> Aunque no se puede especificar un toocreate de grupo de recursos una red virtual (clásica) en uso de PowerShell, Azure crea la red virtual de hello en un grupo de recursos denominado *redes predeterminado*.

---

## <a name="next-steps"></a>Pasos siguientes

- toolearn sobre todo red virtual y la configuración de subred, consulte [administrar redes virtuales](virtual-network-manage-network.md) y [administrar subredes de red virtual](virtual-network-manage-subnet.md). Tienes varias opciones para el uso de redes virtuales y subredes en un requisitos diferentes toomeet del entorno de producción.
- toofilter entrante y saliente el tráfico de subred, crear y aplicar [grupos de seguridad de red](virtual-networks-nsg.md) toosubnets.
- Crear un [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o un [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) máquina virtual y, a continuación, conéctelo tooan de red virtual existente.
- las redes virtuales tooconnect dos en Hola la misma ubicación de Azure, cree un [intercambio de tráfico de red virtual](create-peering-different-deployment-models.md) entre redes virtuales Hola. Puede del mismo nivel de una red virtual (clásica) tooa de red virtual (Administrador de recursos), pero no se puede crear un emparejamiento entre dos redes virtuales (clásicas).
- Conectar hello tooan local red virtual mediante un [puerta de enlace VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o [ExpressRoute de Azure](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuito.
