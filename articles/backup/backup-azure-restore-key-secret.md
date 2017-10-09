---
title: "clave de almacén de claves de aaaRestore y el secreto para cifran máquinas virtuales mediante copia de seguridad de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toorestore clave del almacén de claves y el secreto de copia de seguridad de Azure con PowerShell"
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 45214083-d5fc-4eb3-a367-0239dc59e0f6
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 659b2f647493ffcc9494caee111c8bd584ef9c7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a>Restauración de la clave y el secreto de Key Vault para máquinas virtuales cifradas mediante Azure Backup
En este artículo habla sobre el uso de restauración de copia de seguridad de Azure VM tooperform de cifrado de máquinas virtuales de Azure, si la clave y el secreto no existen en el almacén de claves de Hola. También se pueden utilizar estos pasos si desea toomaintain una copia independiente de clave (Key Encryption Key) y secreto (clave de cifrado de BitLocker) para hello restaura la máquina virtual.

## <a name="prerequisites"></a>Requisitos previos
* **Realizar una copia de seguridad de las máquinas virtuales cifradas**: se realizó una copia de seguridad de las máquinas virtuales cifradas de Azure mediante Azure Backup. Consulte el artículo de hello [administrar copias de seguridad y restauración de máquinas virtuales de Azure con PowerShell](backup-azure-vms-automation.md) para obtener más información acerca de cómo toobackup cifra máquinas virtuales de Azure.
* **Configurar el almacén de claves de Azure** : asegúrese de que el almacén de claves toowhich claves y secretos necesidad toobe restaurar ya está presente. Consulte el artículo de hello [empezar a trabajar con el almacén de claves de Azure](../key-vault/key-vault-get-started.md) para obtener más información acerca de la administración de almacén de claves.
* **Restaurar disco**: asegúrese de que ha desencadenado el trabajo de restauración para restaurar los discos de la máquina virtual cifrada con los [pasos de PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm). Esto es porque este trabajo genera un archivo JSON en la cuenta de almacenamiento que contiene las claves y secretos para hello cifrado VM toobe restaurado.

## <a name="get-key-and-secret-from-azure-backup"></a>Obtención de la clave y el secreto en Azure Backup

> [!NOTE]
> Una vez que se ha restaurado el disco de hello cifradas VM, asegúrese de que:
> 1. $details se rellena con los detalles del trabajo de restauración de disco, como se mencionó en [PowerShell los pasos de la sección de discos de Hola de restauración](backup-azure-vms-automation.md#restore-an-azure-vm)
> 2. Máquina virtual debe crearse desde discos restaurados solo **después de clave y el secreto del almacén de tookey restaurada**.
>
>

Hola consulta restaura propiedades de disco para obtener detalles de trabajo de Hola.

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

Establecer contexto de almacenamiento de Azure de Hola y restaurar el archivo de configuración de JSON que contiene claves y detalles secretos para VM cifrado.

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a>Restauración de la clave
Una vez que se genera el archivo JSON de hello en la ruta de acceso de destino de hello mencionado anteriormente, generar archivo de blob de clave de hello JSON y fuente toorestore cmdlet clave tooput Hola de claves (KEK) en el almacén de claves de Hola.

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a>Restauración del secreto
Utilice un archivo JSON Hola generados por encima del valor y el nombre de secreto tooget y fuente secreto de Hola de tooput tooset cmdlet secreto (BEK) en el almacén de claves de Hola. **Use estos cmdlets si la máquina virtual está cifrada mediante BEK y KEK.**

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

Si la máquina virtual está **cifrado con solo BEK**, generar un archivo blob secreto de hello JSON y fuente secreto de Hola de tooput toorestore cmdlet secreto (BEK) en el almacén de claves de Hola.

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. Valor de $secretname puede obtenerse consultando la salida de toohello de $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl y usando texto después de secretos / p. ej. dirección URL de secreto de salida es https://keyvaultname.vault.azure.net/secrets/ Nombre de B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 y secreto es B3284AAA-DAAA-4AAA-B393-60CAA848AAAA
> 2. Valor de etiqueta de hello DiskEncryptionKeyFileName es el mismo que el nombre de secreto.
>
>

## <a name="create-virtual-machine-from-restored-disk"></a>Creación de la máquina virtual desde el disco restaurado
Si ha hecho VM cifrada mediante copia de seguridad de Azure VM, Hola cmdlets de PowerShell mencionadas anteriormente ayuda que restaurar clave y el almacén de claves de secreto toohello atrás. Después de su restauración, consulte el artículo hello [administrar copias de seguridad y restauración de máquinas virtuales de Azure con PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate cifrar las máquinas virtuales desde disco restaurada, la clave y el secreto.

## <a name="legacy-approach"></a>Enfoque heredado
enfoque de Hello mencionada anteriormente podría funcionar para todos los puntos de recuperación de Hola. Sin embargo, hello enfoque anterior para obtener la clave y la información secreta de punto de recuperación, será válido para los puntos de recuperación anteriores a 11 de julio de 2017 para máquinas virtuales que se cifran mediante BEK y KEK. Una vez completo el trabajo de restauración de disco para la máquina virtual cifrada con los [pasos en PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm), asegúrese de que $rp se rellena con un valor válido.

### <a name="restore-key"></a>Restauración de la clave
Usar hello siguiendo la información de claves (KEK) tooget de cmdlets de punto de recuperación y fuente toorestore cmdlet clave tooput en el almacén de claves de Hola de nuevo.

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a>Restauración del secreto
Usar hello siguiendo la información de secreto (BEK) tooget de cmdlets de punto de recuperación y fuente tooset cmdlet secreto tooput en almacén de claves de Hola de nuevo.

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. Valor de $secretname puede obtenerse consultando la salida de toohello de rp1 $. KeyAndSecretDetails.SecretUrl y el uso de texto después de secretos / p. ej., dirección URL de secreto de salida es https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 y es el nombre de secreto B3284AAA-DAAA-4AAA-B393-60CAA848AAAA
> 2. Valor de etiqueta de hello DiskEncryptionKeyFileName es el mismo que el nombre de secreto.
> 3. Valor de DiskEncryptionKeyEncryptionKeyURL puede obtenerse de almacén de claves después de restaurar las claves de hello volver y usar [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet
>
>

## <a name="next-steps"></a>Pasos siguientes
Después de restaurar la clave y el almacén secreto tookey atrás, consulte el artículo de hello [administrar copias de seguridad y restauración de máquinas virtuales de Azure con PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate cifrar las máquinas virtuales desde disco restaurada, clave y el secreto.
