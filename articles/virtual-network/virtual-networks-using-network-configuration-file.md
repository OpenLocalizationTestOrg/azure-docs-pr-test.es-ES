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
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a>Configuración de una red virtual (clásica) mediante un archivo de configuración de red
> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [el Administrador de recursos y el clásico](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Este artículo incluye el uso de modelo de implementación clásica de Hola. Microsoft recomienda que más nuevas implementaciones utilizarán modelo de implementación del Administrador de recursos de Hola.

Puede crear y configurar una red virtual (clásica) con un archivo de configuración de red mediante hello Azure interfaz de línea de comandos (CLI) 1.0 o Azure PowerShell. No se puede crear o modificar una red virtual a través del modelo de implementación de Azure Resource Manager Hola con un archivo de configuración de red. No se puede usar hello Azure toocreate portal o modificar una red virtual (clásica) con un archivo de configuración de red, pero puede usar Hola toocreate portal Azure una red virtual (clásica), sin utilizar un archivo de configuración de red.

Crear y configurar una red virtual (clásica) con un archivo de configuración de red requieren exportar, cambiar e importar archivo de Hola.

## <a name="export"></a>Exportación de un archivo de configuración de red

También puede usar PowerShell o hello Azure CLI tooexport un archivo de configuración de red. PowerShell exporta un archivo XML, mientras que hello Azure CLI exporta un archivo json.

### <a name="powershell"></a>PowerShell
 
1. [Instale Azure PowerShell e inicie sesión en tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Cambie el directorio de hello (y asegurarse de que exista) y nombre de archivo en hello siguiente comando como deseado y luego ejecución Hola comando tooexport Hola del archivo de configuración:

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a>CLI de Azure 1.0

1. [Instalar hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Completar Hola restantes pasos desde un símbolo del sistema de Azure CLI 1.0.
2. Inicie sesión en tooAzure escribiendo hello `azure login` comando.
3. Asegúrese de que está en modo de asm escribiendo hello `azure config mode asm` comando.
4. Cambie el directorio de hello (y asegurarse de que exista) y nombre de archivo en hello siguiente comando como deseado y luego ejecución Hola comando tooexport Hola del archivo de configuración:
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a>Creación o modificación mediante el archivo de configuración de red

Un archivo de configuración de red es un archivo XML (cuando se usa PowerShell) o un archivo json (cuando se usa Hola CLI de Azure). Puede editar el archivo hello en cualquier texto o editor XML/json. Hola [opciones de esquema de archivo de configuración de red](https://msdn.microsoft.com/library/azure/jj157100.aspx) artículo incluye los detalles de todas las configuraciones. Para una explicación adicional de valores de hello, consulte [ver redes virtuales y la configuración](virtual-network-manage-network.md#view-vnet). cambios de Hola que realice toohello archivo:

- Debe ser compatible con el esquema de Hola o importación de Hola de red, archivo de configuración se producirá un error.
- Sobrescriben cualquier configuración de red existente para su suscripción, por lo que debe tener mucho cuidado al realizar modificaciones. Por ejemplo, hacer referencia a archivos de configuración de red de ejemplo de Hola que siguen. Indicar el archivo original de hello contiene dos **VirtualNetworkSite** instancias y se cambia, tal y como se muestra en los ejemplos de hello. Cuando se importa el archivo hello, Azure elimina la red virtual de Hola para hello **VirtualNetworkSite** instancia quitó en el archivo hello. Este escenario simplificado se da por supuesto que no hay recursos estaban en la red virtual de hello, como si hubiera, no se pudo eliminar la red virtual de Hola y se producirá un error en la importación de Hola.

> [!IMPORTANT]
> Azure considera que una subred que tiene algo implementado tooit como **en uso**. Cuando una subred está en uso, no puede modificarse. Antes de modificar la información de subred en un archivo de configuración de red, mueva todo lo que ha implementado toohello subred tooa otra subred que no se esté modificando. Vea [mover una máquina virtual o instancia de rol tooa otra subred](virtual-networks-move-vm-role-to-subnet.md) para obtener más información.

### <a name="example-xml-for-use-with-powershell"></a>XML de ejemplo para su uso con PowerShell

Hello siguiente archivo de configuración de red en el ejemplo crea una red virtual denominada *myVirtualNetwork* con un espacio de direcciones de *10.0.0.0/16* en hello *UU* Azure región. una subred con el nombre de red virtual de Hello contiene *mySubnet* con un prefijo de dirección de *10.0.0.0/24*.

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

Si Hola del archivo de configuración exportado no contiene ningún contenido, puede copiar Hola XML en el ejemplo anterior de Hola y péguelo en un nuevo archivo.

### <a name="example-json-for-use-with-hello-azure-cli-10"></a>JSON de ejemplo para su uso con hello Azure CLI 1.0

Hello siguiente archivo de configuración de red en el ejemplo crea una red virtual denominada *myVirtualNetwork* con un espacio de direcciones de *10.0.0.0/16* en hello *UU* Azure región. una subred con el nombre de red virtual de Hello contiene *mySubnet* con un prefijo de dirección de *10.0.0.0/24*.

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

Si Hola del archivo de configuración exportado no contiene ningún contenido, puede copiar json hello en el ejemplo anterior de Hola y péguelo en un nuevo archivo.

## <a name="import"></a>Importación de un archivo de configuración de red

También puede usar PowerShell o hello Azure CLI tooimport un archivo de configuración de red. PowerShell importa un archivo XML, mientras que hello Azure CLI importa un archivo json. Si se produce un error en la importación de hello, confirme ese archivo hello es compatible con hello [esquema de configuración de red](https://msdn.microsoft.com/library/azure/jj157100.aspx). 

### <a name="powershell"></a>PowerShell
 
1. [Instale Azure PowerShell e inicie sesión en tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Cambiar el directorio de Hola y nombre de archivo en hello siguiente comando según sea necesario y luego ejecute el archivo de configuración de red de Hola Hola comando tooimport:
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a>CLI de Azure 1.0

1. [Instalar hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Completar Hola restantes pasos desde un símbolo del sistema de Azure CLI 1.0.
2. Inicie sesión en tooAzure escribiendo hello `azure login` comando.
3. Asegúrese de que está en modo de asm escribiendo hello `azure config mode asm` comando.
4. Cambiar el directorio de Hola y nombre de archivo en hello siguiente comando según sea necesario y luego ejecute el archivo de configuración de red de Hola Hola comando tooimport:

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
