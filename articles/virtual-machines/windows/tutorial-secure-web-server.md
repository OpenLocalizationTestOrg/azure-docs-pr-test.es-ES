---
title: certificados aaaSecure IIS con SSL en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosecure Hola IIS web server con certificados SSL en una máquina virtual de Windows en Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/14/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 7a9e0ce07be2f55095fdb5347b64faf5caa4f7e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a>Protección de un servidor web IIS con certificados SSL en una máquina virtual de Windows en Azure
los servidores web toosecure, que puede ser un certificado Secure Sockets más adelante (SSL) utiliza el tráfico web tooencrypt. Estos certificados SSL pueden almacenarse en el almacén de claves de Azure y permiten implementaciones seguras de certificados tooWindows máquinas virtuales (VMs) en Azure. En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Crear una instancia de Azure Key Vault
> * Generar o cargar un almacén de claves de certificado toohello
> * Crear una máquina virtual e instale el servidor web de IIS de Hola
> * Insertar certificado de hello en hello VM y configurar IIS con un enlace SSL

Este tutorial requiere hello Azure PowerShell versión 3.6 o posterior del módulo. Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola. Si necesita tooupgrade, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).


## <a name="overview"></a>Información general
Azure Key Vault protege claves y secretos criptográficos, como certificados y contraseñas. El almacén de claves ayuda a simplificar el proceso de administración de certificados de Hola y permite toomaintain control de claves que tienen acceso a dichos certificados. Puede crear un certificado autofirmado en Key Vault o cargar un certificado de confianza existente que ya posea.

En lugar de usar una imagen de máquina virtual personalizada que incluya los certificados preparados, inserta los certificados en una máquina virtual en ejecución. Este proceso garantiza que los certificados más actualizados de hello están instalados en un servidor web durante la implementación. Si renovar o reemplazar un certificado, no tendrá también toocreate una nueva imagen de máquina virtual personalizada. los certificados más recientes de Hola se insertan automáticamente a medida que cree máquinas virtuales adicionales. Durante el proceso completo de hello, certificados de hello nunca deje Hola plataforma Windows Azure o se exponen en un script, el historial de la línea de comandos o la plantilla.


## <a name="create-an-azure-key-vault"></a>Crear una instancia de Azure Key Vault
Para poder crear una instancia de Key Vault y certificados, cree un grupo de recursos con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroupSecureWeb* en hello *UU* ubicación:

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

Después, cree una instancia de Key Vault con [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault). Cada instancia de Key Vault requiere un nombre único, que debe estar todo en minúsculas. Reemplace `<mykeyvault>` en el siguiente ejemplo con su propio nombre de almacén de claves único de hello:

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a>Generación de un certificado y almacenamiento en Key Vault
Para usarlo en producción, debe importar un certificado válido firmado por un proveedor de confianza con [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate). Para este tutorial, hello en el ejemplo siguiente se muestra cómo puede generar un certificado autofirmado con [agregar AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) que usa Hola directiva de certificado predeterminada de [ Nueva AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy). 

```powershell
$policy = New-AzureKeyVaultCertificatePolicy `
    -SubjectName "CN=www.contoso.com" `
    -SecretContentType "application/x-pkcs12" `
    -IssuerName Self `
    -ValidityInMonths 12

Add-AzureKeyVaultCertificate `
    -VaultName $keyvaultName `
    -Name "mycert" `
    -CertificatePolicy $policy 
```


## <a name="create-a-virtual-machine"></a>de una máquina virtual
Hola a máquina virtual con un nombre de usuario de administrador y una contraseña para el conjunto [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Ahora puede crear Hola VM con [AzureRmVM nuevo](/powershell/module/azurerm.compute/new-azurermvm). Hello ejemplo siguiente crea componentes de red virtual Hola necesario, configuración de hello SO y, a continuación, crea una máquina virtual denominada *myVM*:

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myVnet" `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleRDP"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 443
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleWWW"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name "myNic" `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS2" | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName "myVM" -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName "MicrosoftWindowsServer" `
    -Offer "WindowsServer" -Skus "2016-Datacenter" -Version "latest" | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Create virtual machine
New-AzureRmVM -ResourceGroupName $resourceGroup -Location $location -VM $vmConfig

# Use hello Custom Script Extension tooinstall IIS
Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server -IncludeManagementTools"}'
```

Se tarda unos minutos para hello VM toobe creado. último paso Hello usa Hola extensión de Script personalizado de Azure tooinstall Hola IIS web server con [AzureRmVmExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmextension).


## <a name="add-a-certificate-toovm-from-key-vault"></a>Agregar un tooVM certificado desde el almacén de claves
certificado de hello tooadd de tooa de almacén de claves de máquina virtual, obtener Id. de hello del certificado con [AzureKeyVaultSecret Get](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret). Agregar Hola certificado toohello VM con [AzureRmVMSecret agregar](/powershell/module/azurerm.compute/add-azurermvmsecret):

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-toouse-hello-certificate"></a>Configurar IIS toouse Hola certificado
Use Hola extensión de Script personalizado nuevo con [AzureRmVMExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmextension) configuración de IIS de tooupdate Hola. Esta actualización aplica a certificados de hello insertado desde el almacén de claves tooIIS y configura el enlace de hello web:

```powershell
$PublicSettings = '{
    "fileUris":["https://raw.githubusercontent.com/iainfoulds/azure-samples/master/secure-iis.ps1"],
    "commandToExecute":"powershell -ExecutionPolicy Unrestricted -File secure-iis.ps1"
}'

Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString $publicSettings
```


### <a name="test-hello-secure-web-app"></a>Aplicación de prueba hello web segura
Obtener dirección IP pública de saludo de la máquina virtual con [AzureRmPublicIPAddress Get](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress). Hello en el ejemplo siguiente se obtiene la dirección IP de Hola para `myPublicIP` creado anteriormente:

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

Ahora puede abrir un explorador web y escriba `https://<myPublicIP>` en la barra de direcciones de Hola. Advertencia de seguridad de hello tooaccept si usa un certificado autofirmado, seleccione **detalles** y, a continuación, **ir en la página Web toohello**:

![Aceptar la advertencia de seguridad del explorador web](./media/tutorial-secure-web-server/browser-warning.png)

El sitio Web IIS seguro, a continuación, se muestra como en el siguiente ejemplo de Hola:

![Visualización del sitio IIS seguro en funcionamiento](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a>Pasos siguientes

En este tutorial, protegió un servidor web IIS con un certificado SSL almacenado en Azure Key Vault. Ha aprendido a:

> [!div class="checklist"]
> * Crear una instancia de Azure Key Vault
> * Generar o cargar un almacén de claves de certificado toohello
> * Crear una máquina virtual e instale el servidor web de IIS de Hola
> * Insertar certificado de hello en hello VM y configurar IIS con un enlace SSL

Siga este toosee vínculo pregeneradas ejemplos de script de máquina virtual.

> [!div class="nextstepaction"]
> [Ejemplos de scripts de máquina virtual Windows](./powershell-samples.md)