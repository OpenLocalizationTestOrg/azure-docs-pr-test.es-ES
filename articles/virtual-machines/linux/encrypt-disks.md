---
title: aaaEncrypt discos en una VM de Linux en Azure | Documentos de Microsoft
description: "¿Cómo tooencrypt discos virtuales en una VM de Linux para el uso de seguridad mejoradas Hola 2.0 de CLI de Azure"
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
ms.openlocfilehash: d6197742bc8562630e8395588c072093fc01d614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-linux-vm"></a><span data-ttu-id="8db8d-103">¿Cómo tooencrypt discos virtuales en una VM Linux</span><span class="sxs-lookup"><span data-stu-id="8db8d-103">How tooencrypt virtual disks on a Linux VM</span></span>
<span data-ttu-id="8db8d-104">Para mejorar la seguridad y el cumplimiento de las máquinas virtuales, se pueden cifrar los discos virtuales en Azure.</span><span class="sxs-lookup"><span data-stu-id="8db8d-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="8db8d-105">Los discos se cifran mediante claves criptográficas que están protegidas en Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="8db8d-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="8db8d-106">Estas claves criptográficas se pueden controlar y se puede auditar su uso.</span><span class="sxs-lookup"><span data-stu-id="8db8d-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="8db8d-107">Este artículo detalla cómo tooencrypt discos virtuales en una VM de Linux con Hola 2.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="8db8d-107">This article details how tooencrypt virtual disks on a Linux VM using hello Azure CLI 2.0.</span></span> <span data-ttu-id="8db8d-108">También puede realizar estos pasos con hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8db8d-108">You can also perform these steps with hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="8db8d-109">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="8db8d-109">Quick commands</span></span>
<span data-ttu-id="8db8d-110">Si necesita tooquickly realizar la tarea hello, Hola después Hola de detalles de la sección base comandos tooencrypt discos virtuales en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8db8d-110">If you need tooquickly accomplish hello task, hello following section details hello base commands tooencrypt virtual disks on your VM.</span></span> <span data-ttu-id="8db8d-111">Obtener más información y el contexto de cada paso se encuentran rest Hola de documento de hello, [a partir de aquí](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="8db8d-111">More detailed information and context for each step can be found hello rest of hello document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="8db8d-112">Necesita hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="8db8d-112">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="8db8d-113">En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="8db8d-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="8db8d-114">Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *myKey* y *myVM*.</span><span class="sxs-lookup"><span data-stu-id="8db8d-114">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="8db8d-115">En primer lugar, habilitar el proveedor de almacén de claves de Azure de hello dentro de su suscripción de Azure con [registro de proveedor az](/cli/azure/provider#register) y crear un grupo de recursos con [crear grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="8db8d-115">First, enable hello Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="8db8d-116">Hello en el ejemplo siguiente se crea un nombre de grupo de recursos *myResourceGroup* en hello *eastus* ubicación:</span><span class="sxs-lookup"><span data-stu-id="8db8d-116">hello following example creates a resource group name *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="8db8d-117">Crear un almacén de claves de Azure con [crear az keyvault](/cli/azure/keyvault#create) y habilitar Hola el almacén de claves para su uso con el cifrado del disco.</span><span class="sxs-lookup"><span data-stu-id="8db8d-117">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="8db8d-118">Especifique un nombre de Key Vault único para *keyvault_name* de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="8db8d-118">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="8db8d-119">Cree una clave criptográfica en la instancia de Key Vault con [az keyvault key create](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="8db8d-119">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="8db8d-120">Hello en el ejemplo siguiente se crea una clave denominada *myKey*:</span><span class="sxs-lookup"><span data-stu-id="8db8d-120">hello following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

<span data-ttu-id="8db8d-121">Cree una entidad de servicio mediante Azure Active Directory con [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="8db8d-121">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="8db8d-122">identificadores de entidad de seguridad de servicio de Hola Hola autenticación y el intercambio de claves criptográficas del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="8db8d-122">hello service principal handles hello authentication and exchange of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="8db8d-123">Hola de ejemplo siguiente lee en valores de hello para la entidad de servicio de hello identificador y la contraseña para su uso en los comandos posteriores:</span><span class="sxs-lookup"><span data-stu-id="8db8d-123">hello following example reads in hello values for hello service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="8db8d-124">contraseña de Hello solo se genera cuando creas Hola entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="8db8d-124">hello password is only output when you create hello service principal.</span></span> <span data-ttu-id="8db8d-125">Si lo desea, ver y grabar Hola contraseña (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="8db8d-125">If desired, view and record hello password (`echo $sp_password`).</span></span> <span data-ttu-id="8db8d-126">Puede mostrar las entidades de servicio con el comando [az ad sp list](/cli/azure/ad/sp#list) y consultar información adicional sobre una entidad de servicio específica con [az ad sp show](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="8db8d-126">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="8db8d-127">Establezca permisos en Key Vault con [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="8db8d-127">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="8db8d-128">En el siguiente ejemplo de Hola Hola Id. de entidad de seguridad de servicio proporcionado de hello anterior comando:</span><span class="sxs-lookup"><span data-stu-id="8db8d-128">In hello following example, hello service principal ID is supplied from hello preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

<span data-ttu-id="8db8d-129">Cree una máquina virtual con [az vm create](/cli/azure/vm#create) y conecte un disco de datos de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="8db8d-129">Create a VM with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="8db8d-130">Solo ciertas imágenes de Marketplace admiten el cifrado de discos.</span><span class="sxs-lookup"><span data-stu-id="8db8d-130">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="8db8d-131">Hello en el ejemplo siguiente se crea una máquina virtual denominada `myVM` con un **CentOS 7.2n** imagen:</span><span class="sxs-lookup"><span data-stu-id="8db8d-131">hello following example creates a VM named `myVM` using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="8db8d-132">SSH tooyour VM con Hola `publicIpAddress` se muestra en la salida de hello de hello anterior comando.</span><span class="sxs-lookup"><span data-stu-id="8db8d-132">SSH tooyour VM using hello `publicIpAddress` shown in hello output of hello preceding command.</span></span> <span data-ttu-id="8db8d-133">Crear una partición y un sistema de archivos y, a continuación, montar el disco de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8db8d-133">Create a partition and filesystem, then mount hello data disk.</span></span> <span data-ttu-id="8db8d-134">Para obtener más información, consulte [conectar tooa nuevo disco de VM de Linux toomount hello](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="8db8d-134">For more information, see [Connect tooa Linux VM toomount hello new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="8db8d-135">Cierre la sesión de SSH.</span><span class="sxs-lookup"><span data-stu-id="8db8d-135">Close your SSH session.</span></span>

<span data-ttu-id="8db8d-136">Cifre la máquina virtual con [az vm encryption enable](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="8db8d-136">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="8db8d-137">Hello en el ejemplo siguiente se usa hello `$sp_id` y `$sp_password` variables de hello anterior `ad sp create-for-rbac` comando:</span><span class="sxs-lookup"><span data-stu-id="8db8d-137">hello following example uses hello `$sp_id` and `$sp_password` variables from hello preceding `ad sp create-for-rbac` command:</span></span>

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

<span data-ttu-id="8db8d-138">Tarda algún tiempo para toocomplete de proceso de cifrado de disco Hola.</span><span class="sxs-lookup"><span data-stu-id="8db8d-138">It takes some time for hello disk encryption process toocomplete.</span></span> <span data-ttu-id="8db8d-139">Supervisar el estado de saludo del proceso de hello con [presentación con cifrado vm az](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="8db8d-139">Monitor hello status of hello process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="8db8d-140">Hola estado muestra **EncryptionInProgress**.</span><span class="sxs-lookup"><span data-stu-id="8db8d-140">hello status shows **EncryptionInProgress**.</span></span> <span data-ttu-id="8db8d-141">Espere hasta que el estado de Hola Hola SO disco informes **VMRestartPending**, a continuación, reinicie la máquina virtual con [reinicio de la máquina virtual de az](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="8db8d-141">Wait until hello status for hello OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="8db8d-142">proceso de cifrado de disco Hello se finaliza una durante el proceso de arranque de hello, por lo que espere unos minutos antes de comprobar el estado de Hola de nuevo con el cifrado **presentación con cifrado vm az**:</span><span class="sxs-lookup"><span data-stu-id="8db8d-142">hello disk encryption process is finalized during hello boot process, so wait a few minutes before checking hello status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="8db8d-143">estado de Hello ahora debería notificar disco Hola sistema operativo y disco de datos como **Encrypted**.</span><span class="sxs-lookup"><span data-stu-id="8db8d-143">hello status should now report both hello OS disk and data disk as **Encrypted**.</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="8db8d-144">Introducción al cifrado de discos</span><span class="sxs-lookup"><span data-stu-id="8db8d-144">Overview of disk encryption</span></span>
<span data-ttu-id="8db8d-145">Los discos virtuales en máquinas virtuales Linux se cifran en reposo mediante [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="8db8d-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="8db8d-146">El cifrado de los discos virtuales en Azure no conlleva ningún cargo.</span><span class="sxs-lookup"><span data-stu-id="8db8d-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="8db8d-147">Las claves criptográficas se almacenan en el almacén de claves de Azure mediante la protección de software, o puede importar o generar las claves en módulos de seguridad de Hardware (HSM) de certificados tooFIPS estándares de 140-2 nivel 2.</span><span class="sxs-lookup"><span data-stu-id="8db8d-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="8db8d-148">Estas claves criptográficas se pueden controlar y se puede auditar su uso.</span><span class="sxs-lookup"><span data-stu-id="8db8d-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="8db8d-149">Estas claves criptográficas son tooencrypt usado y descifrar los discos virtuales conectados tooyour máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8db8d-149">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="8db8d-150">Como las máquinas virtuales se encienden y se apagan, una entidad de servicio de Azure Active Directory proporciona un mecanismos seguro para la emisión de estas claves criptográficas.</span><span class="sxs-lookup"><span data-stu-id="8db8d-150">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="8db8d-151">proceso de Hola para cifrar una máquina virtual es como sigue:</span><span class="sxs-lookup"><span data-stu-id="8db8d-151">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="8db8d-152">Cree una clave criptográfica en Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="8db8d-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="8db8d-153">Configurar el número de toobe criptográficos clave de hello utilizable para el cifrado de discos.</span><span class="sxs-lookup"><span data-stu-id="8db8d-153">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="8db8d-154">clave criptográfica de hello tooread de hello almacén de claves de Azure, cree un servicio de Azure Active Directory principal con los permisos adecuados de Hola.</span><span class="sxs-lookup"><span data-stu-id="8db8d-154">tooread hello cryptographic key from hello Azure Key Vault, create an Azure Active Directory service principal with hello appropriate permissions.</span></span>
4. <span data-ttu-id="8db8d-155">Emitir Hola comando tooencrypt los discos virtuales, especificación de entidad de servicio de Azure Active Directory de Hola y adecuado toobe clave criptográfica utilizado.</span><span class="sxs-lookup"><span data-stu-id="8db8d-155">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory service principal and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="8db8d-156">solicitudes de entidad de seguridad de servicio de Azure Active Directory de Hola Hola requiere la clave criptográfica de almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="8db8d-156">hello Azure Active Directory service principal requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="8db8d-157">discos virtuales de Hola se cifran mediante la clave criptográfica de hello proporcionado.</span><span class="sxs-lookup"><span data-stu-id="8db8d-157">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="8db8d-158">Proceso de cifrado</span><span class="sxs-lookup"><span data-stu-id="8db8d-158">Encryption process</span></span>
<span data-ttu-id="8db8d-159">Cifrado del disco se basa en hello adicionales de los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="8db8d-159">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="8db8d-160">**Almacén de claves de Azure** -utilizar claves criptográficas toosafeguard y secretos usados para el proceso de cifrado y descifrado de hello del disco.</span><span class="sxs-lookup"><span data-stu-id="8db8d-160">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span>
  * <span data-ttu-id="8db8d-161">Si ya existe un almacén de Azure Key Vault, puede utilizarlo.</span><span class="sxs-lookup"><span data-stu-id="8db8d-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="8db8d-162">No es necesario toodedicate los discos de tooencrypting de almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="8db8d-162">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="8db8d-163">límites administrativos tooseparate y visibilidad de clave, puede crear un almacén de claves dedicado.</span><span class="sxs-lookup"><span data-stu-id="8db8d-163">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="8db8d-164">**Azure Active Directory** : Hola de identificadores de intercambio seguro de claves cifradas necesarias y autenticación para solicitado acciones.</span><span class="sxs-lookup"><span data-stu-id="8db8d-164">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="8db8d-165">Normalmente, puede usar un almacén existente de Azure Active Directory para hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8db8d-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="8db8d-166">entidad de servicio de Hello proporciona un mecanismo de seguridad toorequest y emitir claves criptográficas de hello adecuado.</span><span class="sxs-lookup"><span data-stu-id="8db8d-166">hello service principal provides a secure mechanism toorequest and be issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="8db8d-167">No está desarrollando una aplicación real que se integrará con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8db8d-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="8db8d-168">Requisitos y limitaciones</span><span class="sxs-lookup"><span data-stu-id="8db8d-168">Requirements and limitations</span></span>
<span data-ttu-id="8db8d-169">Requisitos y escenarios admitidos para el cifrado de discos:</span><span class="sxs-lookup"><span data-stu-id="8db8d-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="8db8d-170">Hola después de servidor Linux SKU - Ubuntu, CentOS, SUSE y SUSE Linux Enterprise Server (SLES) y Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="8db8d-170">hello following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="8db8d-171">Todos los recursos (por ejemplo, el almacén de claves, la cuenta de almacenamiento y VM) deben estar en hello misma región de Azure y la suscripción.</span><span class="sxs-lookup"><span data-stu-id="8db8d-171">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="8db8d-172">Máquinas virtuales estándar de las series A, D, DS, G y GS.</span><span class="sxs-lookup"><span data-stu-id="8db8d-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="8db8d-173">Cifrado del disco no se admite actualmente en hello los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="8db8d-173">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="8db8d-174">Máquina s virtuales de nivel básico</span><span class="sxs-lookup"><span data-stu-id="8db8d-174">Basic tier VMs.</span></span>
* <span data-ttu-id="8db8d-175">Máquinas virtuales creadas mediante el modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="8db8d-175">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="8db8d-176">Deshabilitado del cifrado de disco de sistema operativo en máquinas virtuales Linux.</span><span class="sxs-lookup"><span data-stu-id="8db8d-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="8db8d-177">Actualizar las claves criptográficas de hello en una VM de Linux ya se ha cifrado.</span><span class="sxs-lookup"><span data-stu-id="8db8d-177">Updating hello cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="8db8d-178">Creación de Azure Key Vault y claves</span><span class="sxs-lookup"><span data-stu-id="8db8d-178">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="8db8d-179">Necesita hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="8db8d-179">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="8db8d-180">En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="8db8d-180">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="8db8d-181">Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *myKey* y *myVM*.</span><span class="sxs-lookup"><span data-stu-id="8db8d-181">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="8db8d-182">primer paso de Hello es un almacén de claves de Azure toostore toocreate las claves criptográficas.</span><span class="sxs-lookup"><span data-stu-id="8db8d-182">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="8db8d-183">Almacén de claves de Azure puede almacenar secretos, claves o contraseñas que permiten toosecurely implementan en sus aplicaciones y servicios.</span><span class="sxs-lookup"><span data-stu-id="8db8d-183">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="8db8d-184">Para el cifrado de disco virtual, utilice toostore de almacén de claves una clave criptográfica que es usado tooencrypt o descifrar los discos virtuales.</span><span class="sxs-lookup"><span data-stu-id="8db8d-184">For virtual disk encryption, you use Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="8db8d-185">Habilitar el proveedor de almacén de claves de Azure de hello dentro de su suscripción de Azure con [registro de proveedor az](/cli/azure/provider#register) y crear un grupo de recursos con [crear grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="8db8d-185">Enable hello Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="8db8d-186">Hello en el ejemplo siguiente se crea un nombre de grupo de recursos *myResourceGroup* en hello `eastus` ubicación:</span><span class="sxs-lookup"><span data-stu-id="8db8d-186">hello following example creates a resource group name *myResourceGroup* in hello `eastus` location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="8db8d-187">Hola almacén de claves de Azure que lo contiene hello las claves criptográfico y proceso asociado recursos como almacenamiento y Hola propia máquina virtual deben residir en Hola misma región.</span><span class="sxs-lookup"><span data-stu-id="8db8d-187">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="8db8d-188">Crear un almacén de claves de Azure con [crear az keyvault](/cli/azure/keyvault#create) y habilitar Hola el almacén de claves para su uso con el cifrado del disco.</span><span class="sxs-lookup"><span data-stu-id="8db8d-188">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="8db8d-189">Especifique un nombre de Key Vault único para *keyvault_name* de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="8db8d-189">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="8db8d-190">Puede almacenar las claves criptográficas mediante software o protección del modelo de seguridad de hardware (HSM).</span><span class="sxs-lookup"><span data-stu-id="8db8d-190">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="8db8d-191">Para usar HSM se necesita un almacén premium de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="8db8d-191">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="8db8d-192">Hay un costo adicional toocreating una prima el almacén de claves en lugar de almacén de claves estándar que almacena las claves protegidas por software.</span><span class="sxs-lookup"><span data-stu-id="8db8d-192">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="8db8d-193">toocreate agregar un almacén de claves, premium Hola anterior paso `--sku Premium` toohello comando.</span><span class="sxs-lookup"><span data-stu-id="8db8d-193">toocreate a premium Key Vault, in hello preceding step add `--sku Premium` toohello command.</span></span> <span data-ttu-id="8db8d-194">Hello en el ejemplo siguiente se usa claves protegidas por software ya que hemos creado un almacén de claves estándar.</span><span class="sxs-lookup"><span data-stu-id="8db8d-194">hello following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="8db8d-195">Para los dos modelos de protección, Hola plataforma Windows Azure debe toobe concede acceso toorequest hello las claves criptográficas cuando Hola VM arranca discos virtuales de toodecrypt Hola.</span><span class="sxs-lookup"><span data-stu-id="8db8d-195">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="8db8d-196">Cree una clave criptográfica en la instancia de Key Vault con [az keyvault key create](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="8db8d-196">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="8db8d-197">Hello en el ejemplo siguiente se crea una clave denominada *myKey*:</span><span class="sxs-lookup"><span data-stu-id="8db8d-197">hello following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-hello-azure-active-directory-service-principal"></a><span data-ttu-id="8db8d-198">Crear Hola entidad de servicio de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8db8d-198">Create hello Azure Active Directory service principal</span></span>
<span data-ttu-id="8db8d-199">Cuando los discos virtuales se cifrada o descifrados, especifique una autenticación de cuentas de hello toohandle e intercambio de claves criptográficas del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="8db8d-199">When virtual disks are encrypted or decrypted, you specify an account toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="8db8d-200">Esta cuenta, una entidad de seguridad de servicio de Active Directory de Azure, permite toorequest de la plataforma Windows Azure de Hola Hola adecuada las claves criptográficas en nombre de VM de Hola.</span><span class="sxs-lookup"><span data-stu-id="8db8d-200">This account, an Azure Active Directory service principal, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="8db8d-201">Su suscripción dispone de una instancia de Azure Active Directory predeterminada, aunque muchas organizaciones tienen directorios de Azure Active Directory dedicados.</span><span class="sxs-lookup"><span data-stu-id="8db8d-201">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="8db8d-202">Cree una entidad de servicio mediante Azure Active Directory con [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="8db8d-202">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="8db8d-203">Hola de ejemplo siguiente lee en valores de hello para la entidad de servicio de hello identificador y la contraseña para su uso en los comandos posteriores:</span><span class="sxs-lookup"><span data-stu-id="8db8d-203">hello following example reads in hello values for hello service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="8db8d-204">contraseña de Hello solo se muestra cuando se crea el servicio de hello principal.</span><span class="sxs-lookup"><span data-stu-id="8db8d-204">hello password is only displayed when you create hello service principal.</span></span> <span data-ttu-id="8db8d-205">Si lo desea, ver y grabar Hola contraseña (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="8db8d-205">If desired, view and record hello password (`echo $sp_password`).</span></span> <span data-ttu-id="8db8d-206">Puede mostrar las entidades de servicio con el comando [az ad sp list](/cli/azure/ad/sp#list) y consultar información adicional sobre una entidad de servicio específica con [az ad sp show](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="8db8d-206">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="8db8d-207">toosuccessfully cifrar o descifrar los discos virtuales, permisos de clave cifrado de hello almacenados en el almacén de claves deben ser conjunto toopermit hello Azure Active Directory service principal tooread Hola claves.</span><span class="sxs-lookup"><span data-stu-id="8db8d-207">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory service principal tooread hello keys.</span></span> <span data-ttu-id="8db8d-208">Establezca permisos en Key Vault con [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="8db8d-208">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="8db8d-209">En el siguiente ejemplo de Hola Hola Id. de entidad de seguridad de servicio proporcionado de hello anterior comando:</span><span class="sxs-lookup"><span data-stu-id="8db8d-209">In hello following example, hello service principal ID is supplied from hello preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a><span data-ttu-id="8db8d-210">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="8db8d-210">Create virtual machine</span></span>
<span data-ttu-id="8db8d-211">tooactually cifrar algunos discos virtuales, permite crear una máquina virtual y agregar un disco de datos.</span><span class="sxs-lookup"><span data-stu-id="8db8d-211">tooactually encrypt some virtual disks, lets create a VM and add a data disk.</span></span> <span data-ttu-id="8db8d-212">Crear un tooencrypt VM con [crear vm az](/cli/azure/vm#create) y adjuntar un disco de datos de 5 Gb.</span><span class="sxs-lookup"><span data-stu-id="8db8d-212">Create a VM tooencrypt with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="8db8d-213">Solo ciertas imágenes de Marketplace admiten el cifrado de discos.</span><span class="sxs-lookup"><span data-stu-id="8db8d-213">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="8db8d-214">Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVM* con un **CentOS 7.2n** imagen:</span><span class="sxs-lookup"><span data-stu-id="8db8d-214">hello following example creates a VM named *myVM* using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="8db8d-215">SSH tooyour VM con Hola `publicIpAddress` se muestra en la salida de hello de hello anterior comando.</span><span class="sxs-lookup"><span data-stu-id="8db8d-215">SSH tooyour VM using hello `publicIpAddress` shown in hello output of hello preceding command.</span></span> <span data-ttu-id="8db8d-216">Crear una partición y un sistema de archivos y, a continuación, montar el disco de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8db8d-216">Create a partition and filesystem, then mount hello data disk.</span></span> <span data-ttu-id="8db8d-217">Para obtener más información, consulte [conectar tooa nuevo disco de VM de Linux toomount hello](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="8db8d-217">For more information, see [Connect tooa Linux VM toomount hello new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="8db8d-218">Cierre la sesión de SSH.</span><span class="sxs-lookup"><span data-stu-id="8db8d-218">Close your SSH session.</span></span>


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="8db8d-219">Cifrado de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8db8d-219">Encrypt virtual machine</span></span>
<span data-ttu-id="8db8d-220">discos virtuales de tooencrypt hello, reúne todos los componentes anteriores de hello:</span><span class="sxs-lookup"><span data-stu-id="8db8d-220">tooencrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="8db8d-221">Especificar Hola entidad de servicio de Azure Active Directory y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="8db8d-221">Specify hello Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="8db8d-222">Especificar Hola el almacén de claves toostore Hola metadatos para los discos cifrados.</span><span class="sxs-lookup"><span data-stu-id="8db8d-222">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="8db8d-223">Especifique hello toouse de claves criptográficas para hello real cifrado y descifrado.</span><span class="sxs-lookup"><span data-stu-id="8db8d-223">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="8db8d-224">Especifique si desea que tooencrypt disco de SO hello, discos de datos de Hola o todos.</span><span class="sxs-lookup"><span data-stu-id="8db8d-224">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="8db8d-225">Cifre la máquina virtual con [az vm encryption enable](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="8db8d-225">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="8db8d-226">Hello en el ejemplo siguiente se usa hello `$sp_id` y `$sp_password` variables de hello anterior `ad sp create-for-rbac` comando:</span><span class="sxs-lookup"><span data-stu-id="8db8d-226">hello following example uses hello `$sp_id` and `$sp_password` variables from hello preceding `ad sp create-for-rbac` command:</span></span>

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

<span data-ttu-id="8db8d-227">Tarda algún tiempo para toocomplete de proceso de cifrado de disco Hola.</span><span class="sxs-lookup"><span data-stu-id="8db8d-227">It takes some time for hello disk encryption process toocomplete.</span></span> <span data-ttu-id="8db8d-228">Supervisar el estado de saludo del proceso de hello con [presentación con cifrado vm az](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="8db8d-228">Monitor hello status of hello process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="8db8d-229">Hola de salida es similar toohello siguiente ejemplo truncada:</span><span class="sxs-lookup"><span data-stu-id="8db8d-229">hello output is similar toohello following truncated example:</span></span>

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

<span data-ttu-id="8db8d-230">Espere hasta que el estado de Hola Hola SO disco informes **VMRestartPending**, a continuación, reinicie la máquina virtual con [reinicio de la máquina virtual de az](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="8db8d-230">Wait until hello status for hello OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="8db8d-231">proceso de cifrado de disco Hello se finaliza una durante el proceso de arranque de hello, por lo que espere unos minutos antes de comprobar el estado de Hola de nuevo con el cifrado **presentación con cifrado vm az**:</span><span class="sxs-lookup"><span data-stu-id="8db8d-231">hello disk encryption process is finalized during hello boot process, so wait a few minutes before checking hello status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="8db8d-232">estado de Hello ahora debería notificar disco Hola sistema operativo y disco de datos como **Encrypted**.</span><span class="sxs-lookup"><span data-stu-id="8db8d-232">hello status should now report both hello OS disk and data disk as **Encrypted**.</span></span>


## <a name="add-additional-data-disks"></a><span data-ttu-id="8db8d-233">Adición de discos de datos adicionales</span><span class="sxs-lookup"><span data-stu-id="8db8d-233">Add additional data disks</span></span>
<span data-ttu-id="8db8d-234">Una vez que haya cifrado los discos de datos, puede agregar más adelante discos virtuales adicionales tooyour VM y cifrarlas también.</span><span class="sxs-lookup"><span data-stu-id="8db8d-234">Once you have encrypted your data disks, you can later add additional virtual disks tooyour VM and also encrypt them.</span></span> <span data-ttu-id="8db8d-235">Por ejemplo, permite agregar un segundo tooyour de disco virtual VM como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="8db8d-235">For example, lets add a second virtual disk tooyour VM as follows:</span></span>

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

<span data-ttu-id="8db8d-236">Vuelva a ejecutar Hola comando tooencrypt Hola los discos virtuales como sigue:</span><span class="sxs-lookup"><span data-stu-id="8db8d-236">Re-run hello command tooencrypt hello virtual disks as follows:</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="8db8d-237">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8db8d-237">Next steps</span></span>
* <span data-ttu-id="8db8d-238">Para más información acerca de cómo administrar Azure Key Vault, incluido cómo eliminar claves criptográficas y almacenes, consulte [Administración de Key Vault mediante CLI](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="8db8d-238">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="8db8d-239">Para obtener más información acerca del cifrado de disco, como preparar una tooAzure tooupload personalizado cifrado de VM, consulte [cifrado del disco de Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="8db8d-239">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
