---
title: "aaaEncrypt discos en una máquina virtual de Windows en Azure | Documentos de Microsoft"
description: "¿Cómo tooencrypt discos virtuales en una máquina virtual de Windows para mejorar la seguridad con Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/10/2017
ms.author: iainfou
ms.openlocfilehash: 77c42a67cb57a9dc5fe3159fce0be75e3a965be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-windows-vm"></a>¿Cómo tooencrypt discos virtuales en una máquina virtual de Windows
Para mejorar la seguridad y el cumplimiento de las máquinas virtuales, se pueden cifrar los discos virtuales en Azure. Los discos se cifran mediante claves criptográficas que están protegidas en Azure Key Vault. Estas claves criptográficas se pueden controlar y se puede auditar su uso. Este artículo detalles de cómo tooencrypt discos virtuales en una máquina virtual de Windows con PowerShell de Azure. También puede [cifrar una VM de Linux con hello Azure CLI 2.0](../linux/encrypt-disks.md).

## <a name="overview-of-disk-encryption"></a>Introducción al cifrado de discos
Los discos virtuales en máquinas virtuales de Windows se cifran en reposo mediante BitLocker. El cifrado de los discos virtuales en Azure no conlleva ningún cargo. Las claves criptográficas se almacenan en el almacén de claves de Azure mediante la protección de software, o puede importar o generar las claves en módulos de seguridad de Hardware (HSM) de certificados tooFIPS estándares de 140-2 nivel 2. Estas claves criptográficas son tooencrypt usado y descifrar los discos virtuales conectados tooyour máquina virtual. Estas claves criptográficas se pueden controlar y se puede auditar su uso. Como las máquinas virtuales se encienden y se apagan, una entidad de servicio de Azure Active Directory proporciona un mecanismos seguro para la emisión de estas claves criptográficas.

proceso de Hola para cifrar una máquina virtual es como sigue:

1. Cree una clave criptográfica en Azure Key Vault.
2. Configurar el número de toobe criptográficos clave de hello utilizable para el cifrado de discos.
3. clave criptográfica de hello tooread de hello almacén de claves de Azure, cree un servicio de Azure Active Directory principal con los permisos adecuados de Hola.
4. Emitir Hola comando tooencrypt los discos virtuales, especificación de entidad de servicio de Azure Active Directory de Hola y adecuado toobe clave criptográfica utilizado.
5. solicitudes de entidad de seguridad de servicio de Azure Active Directory de Hola Hola requiere la clave criptográfica de almacén de claves de Azure.
6. discos virtuales de Hola se cifran mediante la clave criptográfica de hello proporcionado.

## <a name="encryption-process"></a>Proceso de cifrado
Cifrado del disco se basa en hello adicionales de los componentes siguientes:

* **Almacén de claves de Azure** -utilizar claves criptográficas toosafeguard y secretos usados para el proceso de cifrado y descifrado de hello del disco. 
  * Si ya existe un almacén de Azure Key Vault, puede utilizarlo. No es necesario toodedicate los discos de tooencrypting de almacén de claves.
  * límites administrativos tooseparate y visibilidad de clave, puede crear un almacén de claves dedicado.
* **Azure Active Directory** : Hola de identificadores de intercambio seguro de claves cifradas necesarias y autenticación para solicitado acciones. 
  * Normalmente, puede usar un almacén existente de Azure Active Directory para hospedar la aplicación.
  * entidad de servicio de Hello proporciona un mecanismo de seguridad toorequest y emitir claves criptográficas de hello adecuado. No está desarrollando una aplicación real que se integrará con Azure Active Directory.

## <a name="requirements-and-limitations"></a>Requisitos y limitaciones
Requisitos y escenarios admitidos para el cifrado de discos:

* Habilitación del cifrado en nuevas máquinas virtuales de Windows desde imágenes de Azure Marketplace o una imagen de disco duro virtual personalizada.
* Habilitación del cifrado en máquinas virtuales de Windows existentes en Azure.
* Habilitación del cifrado en máquinas virtuales de Windows configuradas mediante Espacios de almacenamiento.
* Deshabilitación del cifrado en las unidades de datos y del sistema operativo en máquinas virtuales de Windows.
* Todos los recursos (por ejemplo, el almacén de claves, la cuenta de almacenamiento y VM) deben estar en hello misma región de Azure y la suscripción.
* Nivel estándar de máquinas virtuales, como las máquinas virtuales de la serie A, D, DS, G y GS.

Cifrado del disco no se admite actualmente en hello los escenarios siguientes:

* Máquina s virtuales de nivel básico
* Máquinas virtuales creadas mediante el modelo de implementación de hello clásico.
* Actualizar las claves criptográficas de hello en una máquina virtual ya se ha cifrado.
* Integración con el Servicio de administración de claves local.

## <a name="create-azure-key-vault-and-keys"></a>Creación de Azure Key Vault y claves
Antes de empezar, asegúrese de que esa versión más reciente de Hola de Hola se ha instalado el módulo de PowerShell de Azure. Para obtener más información, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview). A lo largo de los ejemplos de comandos de hello, reemplace todos los parámetros de ejemplo con sus propios nombres, la ubicación y los valores de clave. Hello en los ejemplos siguientes utilizan una convención de *myResourceGroup*, *myKeyVault*, *myVM*, etcetera.

primer paso de Hello es un almacén de claves de Azure toostore toocreate las claves criptográficas. Almacén de claves de Azure puede almacenar secretos, claves o contraseñas que permiten toosecurely implementan en sus aplicaciones y servicios. Para el cifrado de disco virtual, crear un almacén de claves toostore una clave criptográfica que es usado tooencrypt o descifrar los discos virtuales. 

Habilitar el proveedor de almacén de claves de Azure de hello dentro de su suscripción de Azure con [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), a continuación, cree un grupo de recursos con [AzureRmResourceGroup nuevo](/powershell/module/azurerm.resources/new-azurermresourcegroup). Hello en el ejemplo siguiente se crea un nombre de grupo de recursos *myResourceGroup* en hello *UU* ubicación:

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

Hola almacén de claves de Azure que lo contiene hello las claves criptográfico y proceso asociado recursos como almacenamiento y Hola propia máquina virtual deben residir en Hola misma región. Crear un almacén de claves de Azure con [AzureRmKeyVault New](/powershell/module/azurerm.keyvault/new-azurermkeyvault) y habilitar Hola el almacén de claves para su uso con el cifrado del disco. Especifique un nombre de Key Vault único para *keyVaultName* de la siguiente manera:

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

Puede almacenar las claves criptográficas mediante software o protección del modelo de seguridad de hardware (HSM). Para usar HSM se necesita un almacén premium de Key Vault. Hay un costo adicional toocreating una prima el almacén de claves en lugar de almacén de claves estándar que almacena las claves protegidas por software. toocreate un almacén de claves, premium Hola anterior paso Agregar hello *- Sku "Premium"* parámetros. Hello en el ejemplo siguiente se usa claves protegidas por software ya que hemos creado un almacén de claves estándar. 

Para los dos modelos de protección, Hola plataforma Windows Azure debe toobe concede acceso toorequest hello las claves criptográficas cuando Hola VM arranca discos virtuales de toodecrypt Hola. Cree una clave criptográfica en la instancia de Key Vault con [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey). Hello en el ejemplo siguiente se crea una clave denominada *myKey*:

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-hello-azure-active-directory-service-principal"></a>Crear Hola entidad de servicio de Azure Active Directory
Cuando los discos virtuales se cifrada o descifrados, especifique una autenticación de cuentas de hello toohandle e intercambio de claves criptográficas del almacén de claves. Esta cuenta, una entidad de seguridad de servicio de Active Directory de Azure, permite toorequest de la plataforma Windows Azure de Hola Hola adecuada las claves criptográficas en nombre de VM de Hola. Su suscripción dispone de una instancia de Azure Active Directory predeterminada, aunque muchas organizaciones tienen directorios de Azure Active Directory dedicados.

Cree una entidad de seguridad de servicio en Azure Active Directory con [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal). toospecify una contraseña segura, siga hello [restricciones y directivas de contraseña en Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

toosuccessfully cifrar o descifrar los discos virtuales, permisos de clave cifrado de hello almacenados en el almacén de claves deben ser conjunto toopermit hello Azure Active Directory service principal tooread Hola claves. Establezca los permisos en Key Vault con [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a>Create virtual machine
tootest Hola proceso de cifrado, vamos a crear una máquina virtual. Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVM* con un *Windows Server 2016 Datacenter* imagen:

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "mypublicdns$(Get-Random)"

$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$cred = Get-Credential

$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```


## <a name="encrypt-virtual-machine"></a>Cifrado de máquina virtual
discos virtuales de tooencrypt hello, reúne todos los componentes anteriores de hello:

1. Especificar Hola entidad de servicio de Azure Active Directory y una contraseña.
2. Especificar Hola el almacén de claves toostore Hola metadatos para los discos cifrados.
3. Especifique hello toouse de claves criptográficas para hello real cifrado y descifrado.
4. Especifique si desea que tooencrypt disco de SO hello, discos de datos de Hola o todos.

Cifrar la máquina virtual con [AzureRmVMDiskEncryptionExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) con clave de almacén de claves de Azure de Hola y las credenciales principales de servicio de Azure Active Directory. Hello en el ejemplo siguiente se recupera toda la información clave hello, a continuación, cifra Hola máquina virtual denominada *myVM*:

```powershell
$keyVault = Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $rgName;
$diskEncryptionKeyVaultUrl = $keyVault.VaultUri;
$keyVaultResourceId = $keyVault.ResourceId;
$keyEncryptionKeyUrl = (Get-AzureKeyVaultKey -VaultName $keyVaultName -Name myKey).Key.kid;

Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $rgName `
    -VMName $vmName `
    -AadClientID $app.ApplicationId `
    -AadClientSecret $securePassword `
    -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl `
    -DiskEncryptionKeyVaultId $keyVaultResourceId `
    -KeyEncryptionKeyUrl $keyEncryptionKeyUrl `
    -KeyEncryptionKeyVaultId $keyVaultResourceId
```

Aceptar hello toocontinue símbolo del sistema con el cifrado de la máquina virtual de Hola. Hola VM se reinicia durante el proceso de Hola. Una vez que se complete el proceso de cifrado de Hola y Hola máquina virtual se reinicie, revisar el estado de cifrado de hello con [AzureRmVmDiskEncryptionStatus Get](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

Hola de salida es similar toohello siguiente ejemplo:

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a>Pasos siguientes
* Para más información sobre cómo administrar Azure Key Vault, vea [Configuración de Key Vault para máquinas virtuales en Azure Resource Manager](key-vault-setup.md).
* Para obtener más información acerca del cifrado de disco, como preparar una tooAzure tooupload personalizado cifrado de VM, consulte [cifrado del disco de Azure](../../security/azure-security-disk-encryption.md).
