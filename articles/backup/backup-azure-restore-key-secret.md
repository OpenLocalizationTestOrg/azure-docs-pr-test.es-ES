---
title: "Restauración de la clave y el secreto de Key Vault para máquinas virtuales cifradas mediante Azure Backup | Microsoft Docs"
description: Aprenda a restaurar la clave y el secreto de Key Vault en Azure Backup con PowerShell
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
ms.openlocfilehash: f2db3449187d655248b13198b268841052570626
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a><span data-ttu-id="88fbe-103">Restauración de la clave y el secreto de Key Vault para máquinas virtuales cifradas mediante Azure Backup</span><span class="sxs-lookup"><span data-stu-id="88fbe-103">Restore Key Vault key and secret for encrypted VMs using Azure Backup</span></span>
<span data-ttu-id="88fbe-104">En este artículo se explica cómo usar Azure Backup para restaurar máquinas virtuales de Azure cifradas, si su secreto y su clave no existen en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="88fbe-104">This article talks about using Azure VM Backup to perform restore of encrypted Azure VMs, if your key and secret do not exist in the key vault.</span></span> <span data-ttu-id="88fbe-105">Estos pasos también se pueden usar si desea mantener una copia independiente de la clave (clave de cifrado de Key Vault) y el secreto (clave de cifrado de BitLocker) para la máquina virtual restaurada.</span><span class="sxs-lookup"><span data-stu-id="88fbe-105">These steps can also be used if you want to maintain a separate copy of key (Key Encryption Key) and secret (BitLocker Encryption Key) for the restored VM.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88fbe-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="88fbe-106">Prerequisites</span></span>
* <span data-ttu-id="88fbe-107">**Realizar una copia de seguridad de las máquinas virtuales cifradas**: se realizó una copia de seguridad de las máquinas virtuales cifradas de Azure mediante Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="88fbe-107">**Backup encrypted VMs** - Encrypted Azure VMs have been backed up using Azure Backup.</span></span> <span data-ttu-id="88fbe-108">Consulte el artículo [Implementación y administración de copias de seguridad para las máquinas virtuales implementadas según el modelo de Resource Manager mediante PowerShell](backup-azure-vms-automation.md) para más información acerca de cómo hacer una copia de seguridad cifrada de las máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="88fbe-108">Refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md) for details about how to backup encrypted Azure VMs.</span></span>
* <span data-ttu-id="88fbe-109">**Configurar Azure Key Vault**: asegúrese de que ya exista el almacén de claves donde deben restaurarse las claves y los secretos.</span><span class="sxs-lookup"><span data-stu-id="88fbe-109">**Configure Azure Key Vault** – Ensure that key vault to which keys and secrets need to be restored is already present.</span></span> <span data-ttu-id="88fbe-110">Consulte el artículo [Introducción a Azure Key Vault](../key-vault/key-vault-get-started.md) para más información sobre la administración de almacenes de claves.</span><span class="sxs-lookup"><span data-stu-id="88fbe-110">Refer the article [Get Started with Azure Key Vault](../key-vault/key-vault-get-started.md) for details about key vault management.</span></span>
* <span data-ttu-id="88fbe-111">**Restaurar disco**: asegúrese de que ha desencadenado el trabajo de restauración para restaurar los discos de la máquina virtual cifrada con los [pasos de PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="88fbe-111">**Restore disk** - Ensure that you have triggered restore job for restoring disks for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm).</span></span> <span data-ttu-id="88fbe-112">Esto se debe a que este trabajo genera un archivo JSON en la cuenta de almacenamiento que contiene las claves y secretos para la máquina virtual cifrada que se va a restaurar.</span><span class="sxs-lookup"><span data-stu-id="88fbe-112">This is because this job generates a JSON file in your storage account containing keys and secrets for the encrypted VM to be restored.</span></span>

## <a name="get-key-and-secret-from-azure-backup"></a><span data-ttu-id="88fbe-113">Obtención de la clave y el secreto en Azure Backup</span><span class="sxs-lookup"><span data-stu-id="88fbe-113">Get key and secret from Azure Backup</span></span>

> [!NOTE]
> <span data-ttu-id="88fbe-114">Una vez que se haya restaurado el disco de la máquina virtual cifrada, asegúrese de que:</span><span class="sxs-lookup"><span data-stu-id="88fbe-114">Once disk has been restored for the encrypted VM, ensure that:</span></span>
> 1. <span data-ttu-id="88fbe-115">$details se rellena con los detalles del trabajo de restauración de disco, como se mencionó en los [pasos de PowerShell en la sección para restaurar los discos](backup-azure-vms-automation.md#restore-an-azure-vm)</span><span class="sxs-lookup"><span data-stu-id="88fbe-115">$details is populated with restore disk job details, as mentioned in [PowerShell steps in Restore the Disks section](backup-azure-vms-automation.md#restore-an-azure-vm)</span></span>
> 2. <span data-ttu-id="88fbe-116">La máquina virtual debe crearse desde los discos restaurados solo **después de que la clave y el secreto se restauren en el almacén de claves**.</span><span class="sxs-lookup"><span data-stu-id="88fbe-116">VM should be created from restored disks only **after key and secret is restored to key vault**.</span></span>
>
>

<span data-ttu-id="88fbe-117">Realice una consulta destinada a las propiedades de los discos restaurados para obtener los detalles del trabajo.</span><span class="sxs-lookup"><span data-stu-id="88fbe-117">Query the restored disk properties for the job details.</span></span>

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

<span data-ttu-id="88fbe-118">Establezca el contexto de almacenamiento de Azure y restaure el archivo de configuración JSON que contenga los detalles del secreto y la clave para la máquina virtual cifrada.</span><span class="sxs-lookup"><span data-stu-id="88fbe-118">Set the Azure storage context and restore JSON configuration file containing key and secret details for encrypted VM.</span></span>

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a><span data-ttu-id="88fbe-119">Restauración de la clave</span><span class="sxs-lookup"><span data-stu-id="88fbe-119">Restore key</span></span>
<span data-ttu-id="88fbe-120">Una vez que el archivo JSON se genere en la ruta de acceso de destino que se mencionó anteriormente, genere el archivo de blob de clave a partir de JSON y úselo para restaurar el cmdlet de la clave y colocar la clave (KEK) nuevo en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="88fbe-120">Once the JSON file is generated in the destination path mentioned above, generate key blob file from the JSON and feed it to restore key cmdlet to put the key (KEK) back in the key vault.</span></span>

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a><span data-ttu-id="88fbe-121">Restauración del secreto</span><span class="sxs-lookup"><span data-stu-id="88fbe-121">Restore secret</span></span>
<span data-ttu-id="88fbe-122">Use el archivo JSON generado anteriormente para obtener el valor y nombre del secreto, y páselos para establecer el cmdlet del secreto para poner de nuevo el secreto (BEK) en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="88fbe-122">Use the JSON file generated above to get secret name and value and feed it to set secret cmdlet to put the secret (BEK) back in the key vault.</span></span> <span data-ttu-id="88fbe-123">**Use estos cmdlets si la máquina virtual está cifrada mediante BEK y KEK.**</span><span class="sxs-lookup"><span data-stu-id="88fbe-123">**Use these cmdlets if your VM is encrypted using BEK and KEK.**</span></span>

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

<span data-ttu-id="88fbe-124">Si la máquina virtual está **cifrada solo con BEK**, genere un archivo blob secreto a partir del JSON y rellénelo para restaurar el cmdlet secreto con el fin de volver a poner el secreto (BEK) en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="88fbe-124">If your VM is **encrypted using BEK only**, generate secret blob file from the JSON and feed it to restore secret cmdlet to put the secret (BEK) back in the key vault.</span></span>

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. <span data-ttu-id="88fbe-125">El valor de $secretname puede obtenerse haciendo referencia a la salida de $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl y usando el texto después de secrets/. Por ejemplo, la dirección URL de secreto de salida es https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 y el nombre del secreto B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="88fbe-125">Value for $secretname can be obtained by referring to the output of $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="88fbe-126">El valor de la etiqueta DiskEncryptionKeyFileName es igual que el nombre de secreto.</span><span class="sxs-lookup"><span data-stu-id="88fbe-126">Value of the tag DiskEncryptionKeyFileName is same as secret name.</span></span>
>
>

## <a name="create-virtual-machine-from-restored-disk"></a><span data-ttu-id="88fbe-127">Creación de la máquina virtual desde el disco restaurado</span><span class="sxs-lookup"><span data-stu-id="88fbe-127">Create virtual machine from restored disk</span></span>
<span data-ttu-id="88fbe-128">Si ha realizado la copia de seguridad de la máquina virtual cifrada mediante Azure VM Backup, los cmdlets de PowerShell mencionados arriba le ayudan a restaurar la clave y el secreto en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="88fbe-128">If you have backed up encrypted VM using Azure VM Backup, the PowerShell cmdlets mentioned above help you restore key and secret back to the key vault.</span></span> <span data-ttu-id="88fbe-129">Después de restaurarlos, vea el artículo [Administración de copias de seguridad y restauración de las máquinas virtuales de Azure mediante PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) para crear máquinas virtuales cifradas a partir del disco, la clave y el secreto restaurados.</span><span class="sxs-lookup"><span data-stu-id="88fbe-129">After restoring them, refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) to create encrypted VMs from restored disk, key, and secret.</span></span>

## <a name="legacy-approach"></a><span data-ttu-id="88fbe-130">Enfoque heredado</span><span class="sxs-lookup"><span data-stu-id="88fbe-130">Legacy approach</span></span>
<span data-ttu-id="88fbe-131">El enfoque mencionado arriba podría funcionar para todos los puntos de recuperación.</span><span class="sxs-lookup"><span data-stu-id="88fbe-131">The approach mentioned above would work for all the recovery points.</span></span> <span data-ttu-id="88fbe-132">Pero el enfoque anterior de obtener la información de la clave y el secreto desde el punto de recuperación sería válido para los puntos de recuperación anteriores al 11 de julio de 2017 para máquinas virtuales cifradas con BEK y KEK.</span><span class="sxs-lookup"><span data-stu-id="88fbe-132">However, the older approach of getting key and secret information from recovery point, would be valid for recovery points older than July 11, 2017 for VMs encrypted using BEK and KEK.</span></span> <span data-ttu-id="88fbe-133">Una vez completo el trabajo de restauración de disco para la máquina virtual cifrada con los [pasos en PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm), asegúrese de que $rp se rellena con un valor válido.</span><span class="sxs-lookup"><span data-stu-id="88fbe-133">Once restore disk job is complete for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm), ensure that $rp is populated with a valid value.</span></span>

### <a name="restore-key"></a><span data-ttu-id="88fbe-134">Restauración de la clave</span><span class="sxs-lookup"><span data-stu-id="88fbe-134">Restore key</span></span>
<span data-ttu-id="88fbe-135">Use los siguientes cmdlets para obtener la información de claves (KEK) del punto de recuperación y usarla para restaurar el cmdlet de claves y volver a colocarla en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="88fbe-135">Use the following cmdlets to get key (KEK) information from recovery point and feed it to restore key cmdlet to put it back in the key vault.</span></span>

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a><span data-ttu-id="88fbe-136">Restauración del secreto</span><span class="sxs-lookup"><span data-stu-id="88fbe-136">Restore secret</span></span>
<span data-ttu-id="88fbe-137">Use los siguientes cmdlets para obtener la información de secretos (BEK) del punto de recuperación y usarla para establecer el cmdlet de secretos y volver a colocarla en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="88fbe-137">Use the following cmdlets to get secret (BEK) information from recovery point and feed it to set secret cmdlet to put it back in the key vault.</span></span>

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. <span data-ttu-id="88fbe-138">El valor de $secretname puede obtenerse haciendo referencia a la salida de $rp1.KeyAndSecretDetails.SecretUrl y usando el texto después de secrets/. Por ejemplo, la dirección URL de secreto de salida es https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 y el nombre del secreto B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="88fbe-138">Value for $secretname can be obtained by referring to the output of $rp1.KeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="88fbe-139">El valor de la etiqueta DiskEncryptionKeyFileName es igual que el nombre de secreto.</span><span class="sxs-lookup"><span data-stu-id="88fbe-139">Value of the tag DiskEncryptionKeyFileName is same as secret name.</span></span>
> 3. <span data-ttu-id="88fbe-140">El valor de DiskEncryptionKeyEncryptionKeyURL puede obtenerse del almacén de claves después de restaurar las claves y usar el cmdlet [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx).</span><span class="sxs-lookup"><span data-stu-id="88fbe-140">Value for DiskEncryptionKeyEncryptionKeyURL can be obtained from key vault after restoring the keys back and using [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="88fbe-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="88fbe-141">Next steps</span></span>
<span data-ttu-id="88fbe-142">Después de restaurar la clave y el secreto de nuevo en el almacén de claves, consulte el artículo [Administración de copias de seguridad y restauración de las máquinas virtuales de Azure mediante PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) para restaurar las máquinas virtuales cifradas a partir del disco, la clave y el secreto restaurados.</span><span class="sxs-lookup"><span data-stu-id="88fbe-142">After restoring key and secret back to key vault, refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) to create encrypted VMs from restored disk, key and secret.</span></span>
