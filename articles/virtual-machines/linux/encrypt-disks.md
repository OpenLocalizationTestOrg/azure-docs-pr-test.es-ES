---
title: Cifrado de discos en una VM de Linux en Azure | Microsoft Docs
description: Cifrado de discos virtuales en una VM de Linux para mejorar la seguridad con la CLI de Azure 2.0
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2a23b6fa-6941-4998-9804-8efe93b647b3
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: 172b4c8f5c098d776cb689543f5d8f163b8895b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-encrypt-virtual-disks-on-a-linux-vm"></a><span data-ttu-id="be09e-103">Cifrado de discos virtuales en una VM de Linux</span><span class="sxs-lookup"><span data-stu-id="be09e-103">How to encrypt virtual disks on a Linux VM</span></span>
<span data-ttu-id="be09e-104">Para mejorar la seguridad y el cumplimiento de las máquinas virtuales, se pueden cifrar los discos virtuales en Azure.</span><span class="sxs-lookup"><span data-stu-id="be09e-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="be09e-105">Los discos se cifran mediante claves criptográficas que están protegidas en Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="be09e-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="be09e-106">Estas claves criptográficas se pueden controlar y se puede auditar su uso.</span><span class="sxs-lookup"><span data-stu-id="be09e-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="be09e-107">En este artículo se detalla cómo cifrar los discos virtuales en una VM de Linux con la CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="be09e-107">This article details how to encrypt virtual disks on a Linux VM using the Azure CLI 2.0.</span></span> <span data-ttu-id="be09e-108">También puede llevar a cabo estos pasos con la [CLI de Azure 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="be09e-108">You can also perform these steps with the [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="be09e-109">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="be09e-109">Quick commands</span></span>
<span data-ttu-id="be09e-110">Si necesita realizar rápidamente la tarea, en la siguiente sección se detallan los comandos base para cifrar discos virtuales en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="be09e-110">If you need to quickly accomplish the task, the following section details the base commands to encrypt virtual disks on your VM.</span></span> <span data-ttu-id="be09e-111">Se puede encontrar información más detallada y contexto para cada paso en el resto del documento, [comenzando aquí](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="be09e-111">More detailed information and context for each step can be found the rest of the document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="be09e-112">Necesita tener instalada la última versión de la [CLI de Azure 2.0](/cli/azure/install-az-cli2) e iniciar sesión en una cuenta de Azure con [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="be09e-112">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="be09e-113">En los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="be09e-113">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="be09e-114">Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *myKey* y *myVM*.</span><span class="sxs-lookup"><span data-stu-id="be09e-114">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="be09e-115">En primer lugar, habilite el proveedor de Azure Key Vault en su suscripción de Azure con [az provider register](/cli/azure/provider#register) y cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="be09e-115">First, enable the Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="be09e-116">En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroup* en la ubicación *eastus*:</span><span class="sxs-lookup"><span data-stu-id="be09e-116">The following example creates a resource group name *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="be09e-117">Cree una instancia de Azure Key Vault con [az keyvault create](/cli/azure/keyvault#create) y habilite Key Vault para usarlo con el cifrado de discos.</span><span class="sxs-lookup"><span data-stu-id="be09e-117">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable the Key Vault for use with disk encryption.</span></span> <span data-ttu-id="be09e-118">Especifique un nombre de Key Vault único para *keyvault_name* de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="be09e-118">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="be09e-119">Cree una clave criptográfica en la instancia de Key Vault con [az keyvault key create](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="be09e-119">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="be09e-120">En el ejemplo siguiente se crea una clave llamada *myKey*:</span><span class="sxs-lookup"><span data-stu-id="be09e-120">The following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

<span data-ttu-id="be09e-121">Cree una entidad de servicio mediante Azure Active Directory con [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="be09e-121">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="be09e-122">La entidad de servicio administra la autenticación y el intercambio de claves criptográficas desde Key Vault.</span><span class="sxs-lookup"><span data-stu-id="be09e-122">The service principal handles the authentication and exchange of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="be09e-123">En el ejemplo siguiente se leen los valores de la contraseña y el id. de la entidad de servicio para usarlos en comandos posteriores:</span><span class="sxs-lookup"><span data-stu-id="be09e-123">The following example reads in the values for the service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="be09e-124">La contraseña solo se genera cuando crea la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="be09e-124">The password is only output when you create the service principal.</span></span> <span data-ttu-id="be09e-125">Si lo desea, vea y anote la contraseña (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="be09e-125">If desired, view and record the password (`echo $sp_password`).</span></span> <span data-ttu-id="be09e-126">Puede mostrar las entidades de servicio con el comando [az ad sp list](/cli/azure/ad/sp#list) y consultar información adicional sobre una entidad de servicio específica con [az ad sp show](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="be09e-126">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="be09e-127">Establezca permisos en Key Vault con [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="be09e-127">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="be09e-128">En el ejemplo siguiente, el id. de la entidad de servicio se proporciona a partir del comando anterior:</span><span class="sxs-lookup"><span data-stu-id="be09e-128">In the following example, the service principal ID is supplied from the preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

<span data-ttu-id="be09e-129">Cree una máquina virtual con [az vm create](/cli/azure/vm#create) y conecte un disco de datos de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="be09e-129">Create a VM with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="be09e-130">Solo ciertas imágenes de Marketplace admiten el cifrado de discos.</span><span class="sxs-lookup"><span data-stu-id="be09e-130">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="be09e-131">En el ejemplo siguiente se crea una VM llamada `myVM` mediante una imagen de **CentOS 7.2n**:</span><span class="sxs-lookup"><span data-stu-id="be09e-131">The following example creates a VM named `myVM` using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="be09e-132">Use SSH para tener acceso a la máquina virtual con el valor de `publicIpAddress` que se muestra en la salida del comando anterior.</span><span class="sxs-lookup"><span data-stu-id="be09e-132">SSH to your VM using the `publicIpAddress` shown in the output of the preceding command.</span></span> <span data-ttu-id="be09e-133">Cree una partición y un sistema de archivos y, luego, monte el disco de datos.</span><span class="sxs-lookup"><span data-stu-id="be09e-133">Create a partition and filesystem, then mount the data disk.</span></span> <span data-ttu-id="be09e-134">Para más información, consulte la sección sobre cómo [conectarse a una máquina virtual de Linux para montar el disco nuevo](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="be09e-134">For more information, see [Connect to a Linux VM to mount the new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="be09e-135">Cierre la sesión de SSH.</span><span class="sxs-lookup"><span data-stu-id="be09e-135">Close your SSH session.</span></span>

<span data-ttu-id="be09e-136">Cifre la máquina virtual con [az vm encryption enable](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="be09e-136">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="be09e-137">En el ejemplo siguiente se usan las variables `$sp_id` y `$sp_password` del comando `ad sp create-for-rbac` anterior:</span><span class="sxs-lookup"><span data-stu-id="be09e-137">The following example uses the `$sp_id` and `$sp_password` variables from the preceding `ad sp create-for-rbac` command:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

<span data-ttu-id="be09e-138">El proceso de cifrado de disco demora unos minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="be09e-138">It takes some time for the disk encryption process to complete.</span></span> <span data-ttu-id="be09e-139">Supervise el estado del proceso con [az vm encryption show](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="be09e-139">Monitor the status of the process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="be09e-140">El estado aparece como **EncryptionInProgress**.</span><span class="sxs-lookup"><span data-stu-id="be09e-140">The status shows **EncryptionInProgress**.</span></span> <span data-ttu-id="be09e-141">Espere hasta que el estado del disco del SO indique **VMRestartPending** y, luego, reinicie la máquina virtual con [az vm restart](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="be09e-141">Wait until the status for the OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="be09e-142">El proceso de cifrado de disco finaliza durante el proceso de arranque, por lo que debe esperar unos minutos antes de comprobar nuevamente el estado de cifrado con **az vm encryption show**:</span><span class="sxs-lookup"><span data-stu-id="be09e-142">The disk encryption process is finalized during the boot process, so wait a few minutes before checking the status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="be09e-143">El estado ahora debería indicar que tanto el disco del SO como el disco de datos están **cifrados**.</span><span class="sxs-lookup"><span data-stu-id="be09e-143">The status should now report both the OS disk and data disk as **Encrypted**.</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="be09e-144">Introducción al cifrado de discos</span><span class="sxs-lookup"><span data-stu-id="be09e-144">Overview of disk encryption</span></span>
<span data-ttu-id="be09e-145">Los discos virtuales en máquinas virtuales Linux se cifran en reposo mediante [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="be09e-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="be09e-146">El cifrado de los discos virtuales en Azure no conlleva ningún cargo.</span><span class="sxs-lookup"><span data-stu-id="be09e-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="be09e-147">Las claves criptográficas se almacenan en Azure Key Vault con protección de software, o puede importar o generar las claves en módulos de seguridad de hardware (HSM) certificados conforme a las normas FIPS 140-2 de nivel 2.</span><span class="sxs-lookup"><span data-stu-id="be09e-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified to FIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="be09e-148">Estas claves criptográficas se pueden controlar y se puede auditar su uso.</span><span class="sxs-lookup"><span data-stu-id="be09e-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="be09e-149">Las claves criptográficas se usan para cifrar y descifrar los discos virtuales conectados a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="be09e-149">These cryptographic keys are used to encrypt and decrypt virtual disks attached to your VM.</span></span> <span data-ttu-id="be09e-150">Como las máquinas virtuales se encienden y se apagan, una entidad de servicio de Azure Active Directory proporciona un mecanismos seguro para la emisión de estas claves criptográficas.</span><span class="sxs-lookup"><span data-stu-id="be09e-150">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="be09e-151">El proceso para cifrar una máquina virtual es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="be09e-151">The process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="be09e-152">Cree una clave criptográfica en Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="be09e-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="be09e-153">Configure la clave criptográfica para poder utilizarla para el cifrado de discos.</span><span class="sxs-lookup"><span data-stu-id="be09e-153">Configure the cryptographic key to be usable for encrypting disks.</span></span>
3. <span data-ttu-id="be09e-154">Para leer la clave criptográfica de Azure Key Vault, cree una entidad de servicio de Azure Active Directory con los permisos adecuados.</span><span class="sxs-lookup"><span data-stu-id="be09e-154">To read the cryptographic key from the Azure Key Vault, create an Azure Active Directory service principal with the appropriate permissions.</span></span>
4. <span data-ttu-id="be09e-155">Emita el comando para cifrar los discos virtuales y especifique la entidad de servicio de Azure Active Directory y la clave criptográfica adecuada que se deberá usar.</span><span class="sxs-lookup"><span data-stu-id="be09e-155">Issue the command to encrypt your virtual disks, specifying the Azure Active Directory service principal and appropriate cryptographic key to be used.</span></span>
5. <span data-ttu-id="be09e-156">La entidad de servicio de Azure Active Directory solicita la clave criptográfica necesaria a Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="be09e-156">The Azure Active Directory service principal requests the required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="be09e-157">Los discos virtuales se cifran con la clave criptográfica proporcionada.</span><span class="sxs-lookup"><span data-stu-id="be09e-157">The virtual disks are encrypted using the provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="be09e-158">Proceso de cifrado</span><span class="sxs-lookup"><span data-stu-id="be09e-158">Encryption process</span></span>
<span data-ttu-id="be09e-159">El cifrado de discos utiliza los siguientes componentes adicionales:</span><span class="sxs-lookup"><span data-stu-id="be09e-159">Disk encryption relies on the following additional components:</span></span>

* <span data-ttu-id="be09e-160">**Azure Key Vault**: se usa para proteger las claves criptográficas y los secretos usados para el proceso de cifrado y descifrado de discos.</span><span class="sxs-lookup"><span data-stu-id="be09e-160">**Azure Key Vault** - used to safeguard cryptographic keys and secrets used for the disk encryption/decryption process.</span></span>
  * <span data-ttu-id="be09e-161">Si ya existe un almacén de Azure Key Vault, puede utilizarlo.</span><span class="sxs-lookup"><span data-stu-id="be09e-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="be09e-162">No es necesario dedicar un almacén de Key Vault para el cifrado de discos.</span><span class="sxs-lookup"><span data-stu-id="be09e-162">You do not have to dedicate a Key Vault to encrypting disks.</span></span>
  * <span data-ttu-id="be09e-163">Para separar los límites administrativos y la visibilidad de las claves, puede crear un almacén de Key Vault dedicado.</span><span class="sxs-lookup"><span data-stu-id="be09e-163">To separate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="be09e-164">**Azure Active Directory**: controla el intercambio seguro de las claves cifradas necesarias y la autenticación para las acciones solicitadas.</span><span class="sxs-lookup"><span data-stu-id="be09e-164">**Azure Active Directory** - handles the secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="be09e-165">Normalmente, puede usar un almacén existente de Azure Active Directory para hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="be09e-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="be09e-166">La entidad de servicio proporciona un mecanismo seguro para solicitar y recibir las claves criptográficas correspondientes.</span><span class="sxs-lookup"><span data-stu-id="be09e-166">The service principal provides a secure mechanism to request and be issued the appropriate cryptographic keys.</span></span> <span data-ttu-id="be09e-167">No está desarrollando una aplicación real que se integrará con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="be09e-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="be09e-168">Requisitos y limitaciones</span><span class="sxs-lookup"><span data-stu-id="be09e-168">Requirements and limitations</span></span>
<span data-ttu-id="be09e-169">Requisitos y escenarios admitidos para el cifrado de discos:</span><span class="sxs-lookup"><span data-stu-id="be09e-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="be09e-170">Las siguientes SKU de servidor Linux: Ubuntu, CentOS, SUSE y SUSE Linux Enterprise Server (SLES), y Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="be09e-170">The following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="be09e-171">Todos los recursos (por ejemplo: almacén de Key Vault, cuenta de almacenamiento, máquina virtual, etc.) deben pertenecer a la misma región y suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="be09e-171">All resources (such as Key Vault, Storage account, and VM) must be in the same Azure region and subscription.</span></span>
* <span data-ttu-id="be09e-172">Máquinas virtuales estándar de las series A, D, DS, G y GS.</span><span class="sxs-lookup"><span data-stu-id="be09e-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="be09e-173">El cifrado del disco no se admite actualmente en los siguientes escenarios:</span><span class="sxs-lookup"><span data-stu-id="be09e-173">Disk encryption is not currently supported in the following scenarios:</span></span>

* <span data-ttu-id="be09e-174">Máquina s virtuales de nivel básico</span><span class="sxs-lookup"><span data-stu-id="be09e-174">Basic tier VMs.</span></span>
* <span data-ttu-id="be09e-175">Máquinas virtuales creadas con el modelo de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="be09e-175">VMs created using the Classic deployment model.</span></span>
* <span data-ttu-id="be09e-176">Deshabilitado del cifrado de disco de sistema operativo en máquinas virtuales Linux.</span><span class="sxs-lookup"><span data-stu-id="be09e-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="be09e-177">Actualización de las claves criptográficas en una máquina virtual Linux ya cifrada.</span><span class="sxs-lookup"><span data-stu-id="be09e-177">Updating the cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="be09e-178">Creación de Azure Key Vault y claves</span><span class="sxs-lookup"><span data-stu-id="be09e-178">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="be09e-179">Necesita tener instalada la última versión de la [CLI de Azure 2.0](/cli/azure/install-az-cli2) e iniciar sesión en una cuenta de Azure con [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="be09e-179">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="be09e-180">En los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="be09e-180">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="be09e-181">Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *myKey* y *myVM*.</span><span class="sxs-lookup"><span data-stu-id="be09e-181">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="be09e-182">El primer paso es crear un almacén de Azure Key Vault para almacenar las claves criptográficas.</span><span class="sxs-lookup"><span data-stu-id="be09e-182">The first step is to create an Azure Key Vault to store your cryptographic keys.</span></span> <span data-ttu-id="be09e-183">Azure Key Vault puede almacenar claves, secretos o contraseñas que permiten su implementación segura en las aplicaciones y los servicios.</span><span class="sxs-lookup"><span data-stu-id="be09e-183">Azure Key Vault can store keys, secrets, or passwords that allow you to securely implement them in your applications and services.</span></span> <span data-ttu-id="be09e-184">Para el cifrado de discos virtuales, se usa Key Vault para almacenar una clave criptográfica que se utiliza para cifrar o descifrar los discos virtuales.</span><span class="sxs-lookup"><span data-stu-id="be09e-184">For virtual disk encryption, you use Key Vault to store a cryptographic key that is used to encrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="be09e-185">Habilite el proveedor de Azure Key Vault en su suscripción de Azure con [az provider register](/cli/azure/provider#register) y cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="be09e-185">Enable the Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="be09e-186">En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroup* en la ubicación `eastus`:</span><span class="sxs-lookup"><span data-stu-id="be09e-186">The following example creates a resource group name *myResourceGroup* in the `eastus` location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="be09e-187">El almacén de Azure Key Vault que contiene las claves criptográficas y los recursos de proceso asociados, como el almacenamiento y la propia máquina virtual, debe residir en la misma región.</span><span class="sxs-lookup"><span data-stu-id="be09e-187">The Azure Key Vault containing the cryptographic keys and associated compute resources such as storage and the VM itself must reside in the same region.</span></span> <span data-ttu-id="be09e-188">Cree una instancia de Azure Key Vault con [az keyvault create](/cli/azure/keyvault#create) y habilite Key Vault para usarlo con el cifrado de discos.</span><span class="sxs-lookup"><span data-stu-id="be09e-188">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable the Key Vault for use with disk encryption.</span></span> <span data-ttu-id="be09e-189">Especifique un nombre de Key Vault único para *keyvault_name* de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="be09e-189">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="be09e-190">Puede almacenar las claves criptográficas mediante software o protección del modelo de seguridad de hardware (HSM).</span><span class="sxs-lookup"><span data-stu-id="be09e-190">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="be09e-191">Para usar HSM se necesita un almacén premium de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="be09e-191">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="be09e-192">La creación de un almacén premium de Key Vault conlleva un coste, frente al almacén estándar de Key Vault, que almacena las claves protegidas por software.</span><span class="sxs-lookup"><span data-stu-id="be09e-192">There is an additional cost to creating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="be09e-193">Para crear un almacén de Key Vault premium, en el paso anterior, agregue `--sku Premium` al comando.</span><span class="sxs-lookup"><span data-stu-id="be09e-193">To create a premium Key Vault, in the preceding step add `--sku Premium` to the command.</span></span> <span data-ttu-id="be09e-194">En el ejemplo siguiente se usa claves protegidas por software ya que hemos creado un almacén de Key Vault estándar.</span><span class="sxs-lookup"><span data-stu-id="be09e-194">The following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="be09e-195">En ambos modelos de protección, la plataforma Windows Azure debe tener acceso para solicitar las claves criptográficas cuando la máquina virtual arranca para descifrar los discos virtuales.</span><span class="sxs-lookup"><span data-stu-id="be09e-195">For both protection models, the Azure platform needs to be granted access to request the cryptographic keys when the VM boots to decrypt the virtual disks.</span></span> <span data-ttu-id="be09e-196">Cree una clave criptográfica en la instancia de Key Vault con [az keyvault key create](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="be09e-196">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="be09e-197">En el ejemplo siguiente se crea una clave llamada *myKey*:</span><span class="sxs-lookup"><span data-stu-id="be09e-197">The following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-the-azure-active-directory-service-principal"></a><span data-ttu-id="be09e-198">Creación de la entidad de servicio de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="be09e-198">Create the Azure Active Directory service principal</span></span>
<span data-ttu-id="be09e-199">Cuando los discos virtuales se cifran o descifran, se especifica una cuenta para controlar la autenticación y el intercambio de claves criptográficas desde Key Vault.</span><span class="sxs-lookup"><span data-stu-id="be09e-199">When virtual disks are encrypted or decrypted, you specify an account to handle the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="be09e-200">Esta cuenta, una entidad de servicio de Azure Active Directory, permite que la plataforma de Azure solicite las claves criptográficas correspondientes en nombre de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="be09e-200">This account, an Azure Active Directory service principal, allows the Azure platform to request the appropriate cryptographic keys on behalf of the VM.</span></span> <span data-ttu-id="be09e-201">Su suscripción dispone de una instancia de Azure Active Directory predeterminada, aunque muchas organizaciones tienen directorios de Azure Active Directory dedicados.</span><span class="sxs-lookup"><span data-stu-id="be09e-201">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="be09e-202">Cree una entidad de servicio mediante Azure Active Directory con [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="be09e-202">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="be09e-203">En el ejemplo siguiente se leen los valores de la contraseña y el id. de la entidad de servicio para usarlos en comandos posteriores:</span><span class="sxs-lookup"><span data-stu-id="be09e-203">The following example reads in the values for the service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="be09e-204">La contraseña solo se muestra cuando crea la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="be09e-204">The password is only displayed when you create the service principal.</span></span> <span data-ttu-id="be09e-205">Si lo desea, vea y anote la contraseña (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="be09e-205">If desired, view and record the password (`echo $sp_password`).</span></span> <span data-ttu-id="be09e-206">Puede mostrar las entidades de servicio con el comando [az ad sp list](/cli/azure/ad/sp#list) y consultar información adicional sobre una entidad de servicio específica con [az ad sp show](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="be09e-206">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="be09e-207">Para cifrar o descifrar los discos virtuales correctamente, debe establecer los permisos de la clave criptográfica que se almacena en Key Vault para que permitan que la entidad de servicio de Azure Active Directory lea las claves.</span><span class="sxs-lookup"><span data-stu-id="be09e-207">To successfully encrypt or decrypt virtual disks, permissions on the cryptographic key stored in Key Vault must be set to permit the Azure Active Directory service principal to read the keys.</span></span> <span data-ttu-id="be09e-208">Establezca permisos en Key Vault con [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="be09e-208">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="be09e-209">En el ejemplo siguiente, el id. de la entidad de servicio se proporciona a partir del comando anterior:</span><span class="sxs-lookup"><span data-stu-id="be09e-209">In the following example, the service principal ID is supplied from the preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a><span data-ttu-id="be09e-210">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="be09e-210">Create virtual machine</span></span>
<span data-ttu-id="be09e-211">Para cifrar realmente algunos discos virtuales, vamos a crear una máquina virtual y agregar un disco de datos.</span><span class="sxs-lookup"><span data-stu-id="be09e-211">To actually encrypt some virtual disks, lets create a VM and add a data disk.</span></span> <span data-ttu-id="be09e-212">Cree una máquina virtual con [az vm create](/cli/azure/vm#create) para cifrar y conecte un disco de datos de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="be09e-212">Create a VM to encrypt with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="be09e-213">Solo ciertas imágenes de Marketplace admiten el cifrado de discos.</span><span class="sxs-lookup"><span data-stu-id="be09e-213">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="be09e-214">En el ejemplo siguiente se crea una máquina virtual llamada *myVM* mediante una imagen de **CentOS 7.2n**:</span><span class="sxs-lookup"><span data-stu-id="be09e-214">The following example creates a VM named *myVM* using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="be09e-215">Use SSH para tener acceso a la máquina virtual con el valor de `publicIpAddress` que se muestra en la salida del comando anterior.</span><span class="sxs-lookup"><span data-stu-id="be09e-215">SSH to your VM using the `publicIpAddress` shown in the output of the preceding command.</span></span> <span data-ttu-id="be09e-216">Cree una partición y un sistema de archivos y, luego, monte el disco de datos.</span><span class="sxs-lookup"><span data-stu-id="be09e-216">Create a partition and filesystem, then mount the data disk.</span></span> <span data-ttu-id="be09e-217">Para más información, consulte la sección sobre cómo [conectarse a una máquina virtual de Linux para montar el disco nuevo](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="be09e-217">For more information, see [Connect to a Linux VM to mount the new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="be09e-218">Cierre la sesión de SSH.</span><span class="sxs-lookup"><span data-stu-id="be09e-218">Close your SSH session.</span></span>


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="be09e-219">Cifrado de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="be09e-219">Encrypt virtual machine</span></span>
<span data-ttu-id="be09e-220">Para cifrar los discos virtuales, reúna todos los componentes anteriores:</span><span class="sxs-lookup"><span data-stu-id="be09e-220">To encrypt the virtual disks, you bring together all the previous components:</span></span>

1. <span data-ttu-id="be09e-221">Especifique la entidad de servicio de Azure Active Directory y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="be09e-221">Specify the Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="be09e-222">Especifique el almacén de Key Vault donde se almacenarán los metadatos de los discos cifrados.</span><span class="sxs-lookup"><span data-stu-id="be09e-222">Specify the Key Vault to store the metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="be09e-223">Especifique las claves criptográficas que se utilizarán para el cifrado y descifrado.</span><span class="sxs-lookup"><span data-stu-id="be09e-223">Specify the cryptographic keys to use for the actual encryption and decryption.</span></span>
4. <span data-ttu-id="be09e-224">Especifique si desea cifrar el disco del sistema operativo, los discos de datos o todos.</span><span class="sxs-lookup"><span data-stu-id="be09e-224">Specify whether you want to encrypt the OS disk, the data disks, or all.</span></span>

<span data-ttu-id="be09e-225">Cifre la máquina virtual con [az vm encryption enable](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="be09e-225">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="be09e-226">En el ejemplo siguiente se usan las variables `$sp_id` y `$sp_password` del comando `ad sp create-for-rbac` anterior:</span><span class="sxs-lookup"><span data-stu-id="be09e-226">The following example uses the `$sp_id` and `$sp_password` variables from the preceding `ad sp create-for-rbac` command:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

<span data-ttu-id="be09e-227">El proceso de cifrado de disco demora unos minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="be09e-227">It takes some time for the disk encryption process to complete.</span></span> <span data-ttu-id="be09e-228">Supervise el estado del proceso con [az vm encryption show](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="be09e-228">Monitor the status of the process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="be09e-229">La salida es similar a la del siguiente ejemplo truncado:</span><span class="sxs-lookup"><span data-stu-id="be09e-229">The output is similar to the following truncated example:</span></span>

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

<span data-ttu-id="be09e-230">Espere hasta que el estado del disco del SO indique **VMRestartPending** y, luego, reinicie la máquina virtual con [az vm restart](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="be09e-230">Wait until the status for the OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="be09e-231">El proceso de cifrado de disco finaliza durante el proceso de arranque, por lo que debe esperar unos minutos antes de comprobar nuevamente el estado de cifrado con **az vm encryption show**:</span><span class="sxs-lookup"><span data-stu-id="be09e-231">The disk encryption process is finalized during the boot process, so wait a few minutes before checking the status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="be09e-232">El estado ahora debería indicar que tanto el disco del SO como el disco de datos están **cifrados**.</span><span class="sxs-lookup"><span data-stu-id="be09e-232">The status should now report both the OS disk and data disk as **Encrypted**.</span></span>


## <a name="add-additional-data-disks"></a><span data-ttu-id="be09e-233">Adición de discos de datos adicionales</span><span class="sxs-lookup"><span data-stu-id="be09e-233">Add additional data disks</span></span>
<span data-ttu-id="be09e-234">Una vez cifrados los discos de datos, más adelante podrá agregar más discos virtuales a la máquina virtual, y también cifrarlos.</span><span class="sxs-lookup"><span data-stu-id="be09e-234">Once you have encrypted your data disks, you can later add additional virtual disks to your VM and also encrypt them.</span></span> <span data-ttu-id="be09e-235">Por ejemplo, vamos a agregar un segundo disco virtual a la máquina virtual de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="be09e-235">For example, lets add a second virtual disk to your VM as follows:</span></span>

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

<span data-ttu-id="be09e-236">Vuelva a ejecutar el comando para cifrar los discos virtuales como sigue:</span><span class="sxs-lookup"><span data-stu-id="be09e-236">Re-run the command to encrypt the virtual disks as follows:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```


## <a name="next-steps"></a><span data-ttu-id="be09e-237">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="be09e-237">Next steps</span></span>
* <span data-ttu-id="be09e-238">Para más información acerca de cómo administrar Azure Key Vault, incluido cómo eliminar claves criptográficas y almacenes, consulte [Administración de Key Vault mediante CLI](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="be09e-238">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="be09e-239">Para obtener más información acerca del cifrado de discos, por ejemplo, cómo preparar una máquina virtual personalizada cifrada para cargar en Azure, consulte [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="be09e-239">For more information about disk encryption, such as preparing an encrypted custom VM to upload to Azure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
