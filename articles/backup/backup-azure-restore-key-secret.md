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
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a><span data-ttu-id="a2394-103">Restauración de la clave y el secreto de Key Vault para máquinas virtuales cifradas mediante Azure Backup</span><span class="sxs-lookup"><span data-stu-id="a2394-103">Restore Key Vault key and secret for encrypted VMs using Azure Backup</span></span>
<span data-ttu-id="a2394-104">En este artículo habla sobre el uso de restauración de copia de seguridad de Azure VM tooperform de cifrado de máquinas virtuales de Azure, si la clave y el secreto no existen en el almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2394-104">This article talks about using Azure VM Backup tooperform restore of encrypted Azure VMs, if your key and secret do not exist in hello key vault.</span></span> <span data-ttu-id="a2394-105">También se pueden utilizar estos pasos si desea toomaintain una copia independiente de clave (Key Encryption Key) y secreto (clave de cifrado de BitLocker) para hello restaura la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a2394-105">These steps can also be used if you want toomaintain a separate copy of key (Key Encryption Key) and secret (BitLocker Encryption Key) for hello restored VM.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2394-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a2394-106">Prerequisites</span></span>
* <span data-ttu-id="a2394-107">**Realizar una copia de seguridad de las máquinas virtuales cifradas**: se realizó una copia de seguridad de las máquinas virtuales cifradas de Azure mediante Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="a2394-107">**Backup encrypted VMs** - Encrypted Azure VMs have been backed up using Azure Backup.</span></span> <span data-ttu-id="a2394-108">Consulte el artículo de hello [administrar copias de seguridad y restauración de máquinas virtuales de Azure con PowerShell](backup-azure-vms-automation.md) para obtener más información acerca de cómo toobackup cifra máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="a2394-108">Refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md) for details about how toobackup encrypted Azure VMs.</span></span>
* <span data-ttu-id="a2394-109">**Configurar el almacén de claves de Azure** : asegúrese de que el almacén de claves toowhich claves y secretos necesidad toobe restaurar ya está presente.</span><span class="sxs-lookup"><span data-stu-id="a2394-109">**Configure Azure Key Vault** – Ensure that key vault toowhich keys and secrets need toobe restored is already present.</span></span> <span data-ttu-id="a2394-110">Consulte el artículo de hello [empezar a trabajar con el almacén de claves de Azure](../key-vault/key-vault-get-started.md) para obtener más información acerca de la administración de almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="a2394-110">Refer hello article [Get Started with Azure Key Vault](../key-vault/key-vault-get-started.md) for details about key vault management.</span></span>
* <span data-ttu-id="a2394-111">**Restaurar disco**: asegúrese de que ha desencadenado el trabajo de restauración para restaurar los discos de la máquina virtual cifrada con los [pasos de PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="a2394-111">**Restore disk** - Ensure that you have triggered restore job for restoring disks for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm).</span></span> <span data-ttu-id="a2394-112">Esto es porque este trabajo genera un archivo JSON en la cuenta de almacenamiento que contiene las claves y secretos para hello cifrado VM toobe restaurado.</span><span class="sxs-lookup"><span data-stu-id="a2394-112">This is because this job generates a JSON file in your storage account containing keys and secrets for hello encrypted VM toobe restored.</span></span>

## <a name="get-key-and-secret-from-azure-backup"></a><span data-ttu-id="a2394-113">Obtención de la clave y el secreto en Azure Backup</span><span class="sxs-lookup"><span data-stu-id="a2394-113">Get key and secret from Azure Backup</span></span>

> [!NOTE]
> <span data-ttu-id="a2394-114">Una vez que se ha restaurado el disco de hello cifradas VM, asegúrese de que:</span><span class="sxs-lookup"><span data-stu-id="a2394-114">Once disk has been restored for hello encrypted VM, ensure that:</span></span>
> 1. <span data-ttu-id="a2394-115">$details se rellena con los detalles del trabajo de restauración de disco, como se mencionó en [PowerShell los pasos de la sección de discos de Hola de restauración](backup-azure-vms-automation.md#restore-an-azure-vm)</span><span class="sxs-lookup"><span data-stu-id="a2394-115">$details is populated with restore disk job details, as mentioned in [PowerShell steps in Restore hello Disks section](backup-azure-vms-automation.md#restore-an-azure-vm)</span></span>
> 2. <span data-ttu-id="a2394-116">Máquina virtual debe crearse desde discos restaurados solo **después de clave y el secreto del almacén de tookey restaurada**.</span><span class="sxs-lookup"><span data-stu-id="a2394-116">VM should be created from restored disks only **after key and secret is restored tookey vault**.</span></span>
>
>

<span data-ttu-id="a2394-117">Hola consulta restaura propiedades de disco para obtener detalles de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2394-117">Query hello restored disk properties for hello job details.</span></span>

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

<span data-ttu-id="a2394-118">Establecer contexto de almacenamiento de Azure de Hola y restaurar el archivo de configuración de JSON que contiene claves y detalles secretos para VM cifrado.</span><span class="sxs-lookup"><span data-stu-id="a2394-118">Set hello Azure storage context and restore JSON configuration file containing key and secret details for encrypted VM.</span></span>

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a><span data-ttu-id="a2394-119">Restauración de la clave</span><span class="sxs-lookup"><span data-stu-id="a2394-119">Restore key</span></span>
<span data-ttu-id="a2394-120">Una vez que se genera el archivo JSON de hello en la ruta de acceso de destino de hello mencionado anteriormente, generar archivo de blob de clave de hello JSON y fuente toorestore cmdlet clave tooput Hola de claves (KEK) en el almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2394-120">Once hello JSON file is generated in hello destination path mentioned above, generate key blob file from hello JSON and feed it toorestore key cmdlet tooput hello key (KEK) back in hello key vault.</span></span>

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a><span data-ttu-id="a2394-121">Restauración del secreto</span><span class="sxs-lookup"><span data-stu-id="a2394-121">Restore secret</span></span>
<span data-ttu-id="a2394-122">Utilice un archivo JSON Hola generados por encima del valor y el nombre de secreto tooget y fuente secreto de Hola de tooput tooset cmdlet secreto (BEK) en el almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2394-122">Use hello JSON file generated above tooget secret name and value and feed it tooset secret cmdlet tooput hello secret (BEK) back in hello key vault.</span></span> <span data-ttu-id="a2394-123">**Use estos cmdlets si la máquina virtual está cifrada mediante BEK y KEK.**</span><span class="sxs-lookup"><span data-stu-id="a2394-123">**Use these cmdlets if your VM is encrypted using BEK and KEK.**</span></span>

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

<span data-ttu-id="a2394-124">Si la máquina virtual está **cifrado con solo BEK**, generar un archivo blob secreto de hello JSON y fuente secreto de Hola de tooput toorestore cmdlet secreto (BEK) en el almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2394-124">If your VM is **encrypted using BEK only**, generate secret blob file from hello JSON and feed it toorestore secret cmdlet tooput hello secret (BEK) back in hello key vault.</span></span>

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. <span data-ttu-id="a2394-125">Valor de $secretname puede obtenerse consultando la salida de toohello de $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl y usando texto después de secretos / p. ej. dirección URL de secreto de salida es https://keyvaultname.vault.azure.net/secrets/ Nombre de B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 y secreto es B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="a2394-125">Value for $secretname can be obtained by referring toohello output of $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="a2394-126">Valor de etiqueta de hello DiskEncryptionKeyFileName es el mismo que el nombre de secreto.</span><span class="sxs-lookup"><span data-stu-id="a2394-126">Value of hello tag DiskEncryptionKeyFileName is same as secret name.</span></span>
>
>

## <a name="create-virtual-machine-from-restored-disk"></a><span data-ttu-id="a2394-127">Creación de la máquina virtual desde el disco restaurado</span><span class="sxs-lookup"><span data-stu-id="a2394-127">Create virtual machine from restored disk</span></span>
<span data-ttu-id="a2394-128">Si ha hecho VM cifrada mediante copia de seguridad de Azure VM, Hola cmdlets de PowerShell mencionadas anteriormente ayuda que restaurar clave y el almacén de claves de secreto toohello atrás.</span><span class="sxs-lookup"><span data-stu-id="a2394-128">If you have backed up encrypted VM using Azure VM Backup, hello PowerShell cmdlets mentioned above help you restore key and secret back toohello key vault.</span></span> <span data-ttu-id="a2394-129">Después de su restauración, consulte el artículo hello [administrar copias de seguridad y restauración de máquinas virtuales de Azure con PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate cifrar las máquinas virtuales desde disco restaurada, la clave y el secreto.</span><span class="sxs-lookup"><span data-stu-id="a2394-129">After restoring them, refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate encrypted VMs from restored disk, key, and secret.</span></span>

## <a name="legacy-approach"></a><span data-ttu-id="a2394-130">Enfoque heredado</span><span class="sxs-lookup"><span data-stu-id="a2394-130">Legacy approach</span></span>
<span data-ttu-id="a2394-131">enfoque de Hello mencionada anteriormente podría funcionar para todos los puntos de recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2394-131">hello approach mentioned above would work for all hello recovery points.</span></span> <span data-ttu-id="a2394-132">Sin embargo, hello enfoque anterior para obtener la clave y la información secreta de punto de recuperación, será válido para los puntos de recuperación anteriores a 11 de julio de 2017 para máquinas virtuales que se cifran mediante BEK y KEK.</span><span class="sxs-lookup"><span data-stu-id="a2394-132">However, hello older approach of getting key and secret information from recovery point, would be valid for recovery points older than July 11, 2017 for VMs encrypted using BEK and KEK.</span></span> <span data-ttu-id="a2394-133">Una vez completo el trabajo de restauración de disco para la máquina virtual cifrada con los [pasos en PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm), asegúrese de que $rp se rellena con un valor válido.</span><span class="sxs-lookup"><span data-stu-id="a2394-133">Once restore disk job is complete for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm), ensure that $rp is populated with a valid value.</span></span>

### <a name="restore-key"></a><span data-ttu-id="a2394-134">Restauración de la clave</span><span class="sxs-lookup"><span data-stu-id="a2394-134">Restore key</span></span>
<span data-ttu-id="a2394-135">Usar hello siguiendo la información de claves (KEK) tooget de cmdlets de punto de recuperación y fuente toorestore cmdlet clave tooput en el almacén de claves de Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="a2394-135">Use hello following cmdlets tooget key (KEK) information from recovery point and feed it toorestore key cmdlet tooput it back in hello key vault.</span></span>

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a><span data-ttu-id="a2394-136">Restauración del secreto</span><span class="sxs-lookup"><span data-stu-id="a2394-136">Restore secret</span></span>
<span data-ttu-id="a2394-137">Usar hello siguiendo la información de secreto (BEK) tooget de cmdlets de punto de recuperación y fuente tooset cmdlet secreto tooput en almacén de claves de Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="a2394-137">Use hello following cmdlets tooget secret (BEK) information from recovery point and feed it tooset secret cmdlet tooput it back in hello key vault.</span></span>

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. <span data-ttu-id="a2394-138">Valor de $secretname puede obtenerse consultando la salida de toohello de rp1 $. KeyAndSecretDetails.SecretUrl y el uso de texto después de secretos / p. ej., dirección URL de secreto de salida es https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 y es el nombre de secreto B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="a2394-138">Value for $secretname can be obtained by referring toohello output of $rp1.KeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="a2394-139">Valor de etiqueta de hello DiskEncryptionKeyFileName es el mismo que el nombre de secreto.</span><span class="sxs-lookup"><span data-stu-id="a2394-139">Value of hello tag DiskEncryptionKeyFileName is same as secret name.</span></span>
> 3. <span data-ttu-id="a2394-140">Valor de DiskEncryptionKeyEncryptionKeyURL puede obtenerse de almacén de claves después de restaurar las claves de hello volver y usar [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span><span class="sxs-lookup"><span data-stu-id="a2394-140">Value for DiskEncryptionKeyEncryptionKeyURL can be obtained from key vault after restoring hello keys back and using [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="a2394-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a2394-141">Next steps</span></span>
<span data-ttu-id="a2394-142">Después de restaurar la clave y el almacén secreto tookey atrás, consulte el artículo de hello [administrar copias de seguridad y restauración de máquinas virtuales de Azure con PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate cifrar las máquinas virtuales desde disco restaurada, clave y el secreto.</span><span class="sxs-lookup"><span data-stu-id="a2394-142">After restoring key and secret back tookey vault, refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate encrypted VMs from restored disk, key and secret.</span></span>
