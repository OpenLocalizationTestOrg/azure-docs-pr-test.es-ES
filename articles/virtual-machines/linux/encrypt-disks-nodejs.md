---
title: aaaEncrypt discos en una VM de Linux con hello 1.0 de CLI de Azure | Documentos de Microsoft
description: "¿Cómo tooencrypt discos en una VM de Linux con Hola 1.0 de CLI de Azure y modelo de implementación del Administrador de recursos de Hola"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/06/2017
ms.author: iainfou
ms.openlocfilehash: 68a0394d366c3c6941e2c6db0d4263123f951946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-disks-on-a-linux-vm-using-hello-azure-cli-10"></a><span data-ttu-id="3f5ff-103">Cifrar discos en una VM de Linux con hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="3f5ff-103">Encrypt disks on a Linux VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="3f5ff-104">Para mejorar la seguridad y el cumplimiento de las máquinas virtuales, los discos virtuales en Azure se pueden cifrar en reposo.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted at rest.</span></span> <span data-ttu-id="3f5ff-105">Los discos se cifran mediante claves criptográficas que están protegidas en Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="3f5ff-106">Estas claves criptográficas se pueden controlar y se puede auditar su uso.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="3f5ff-107">Este artículo detalla cómo tooencrypt discos virtuales en una VM de Linux con Hola 1.0 de CLI de Azure y modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-107">This article details how tooencrypt virtual disks on a Linux VM using hello Azure CLI 1.0 and hello Resource Manager deployment model.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="3f5ff-108">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="3f5ff-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="3f5ff-109">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="3f5ff-110">[Azure 1.0 de CLI](#quick-commands) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="3f5ff-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="3f5ff-111">[Azure 2.0 CLI](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="3f5ff-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="3f5ff-112">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="3f5ff-112">Quick commands</span></span>
<span data-ttu-id="3f5ff-113">Si necesita tooquickly realizar la tarea hello, Hola después Hola de detalles de la sección base comandos tooencrypt discos virtuales en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-113">If you need tooquickly accomplish hello task, hello following section details hello base commands tooencrypt virtual disks on your VM.</span></span> <span data-ttu-id="3f5ff-114">Obtener más información y el contexto de cada paso se encuentran rest Hola de documento de hello, [a partir de aquí](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="3f5ff-114">More detailed information and context for each step can be found hello rest of hello document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="3f5ff-115">Necesita hello [más reciente 1.0 de CLI de Azure](../../xplat-cli-install.md) instalado e inició sesión mediante el modo de administrador de recursos de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-115">You need hello [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="3f5ff-116">En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-116">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="3f5ff-117">Los nombres de parámetros de ejemplo incluyen `myResourceGroup`, `myKeyVault` y `myVM`.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-117">Example parameter names include `myResourceGroup`, `myKeyVault`, and `myVM`.</span></span>

<span data-ttu-id="3f5ff-118">En primer lugar, habilitar el proveedor de almacén de claves de Azure de hello dentro de su suscripción de Azure y crear un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-118">First, enable hello Azure Key Vault provider within your Azure subscription and create a resource group.</span></span> <span data-ttu-id="3f5ff-119">Hello en el ejemplo siguiente se crea un nombre de grupo de recursos `myResourceGroup` en hello `WestUS` ubicación:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-119">hello following example creates a resource group name `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="3f5ff-120">Cree un almacén de Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-120">Create an Azure Key Vault.</span></span> <span data-ttu-id="3f5ff-121">Hello en el ejemplo siguiente se crea un almacén de claves denominado `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-121">hello following example creates a Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="3f5ff-122">Cree una clave criptográfica en su almacén de Key Vault y habilítela para el cifrado de discos.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-122">Create a cryptographic key in your Key Vault and enable it for disk encryption.</span></span> <span data-ttu-id="3f5ff-123">Hello en el ejemplo siguiente se crea una clave denominada `myKey`:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-123">hello following example creates a key named `myKey`:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

<span data-ttu-id="3f5ff-124">Crear un punto de conexión con Azure Active Directory para controlar la autenticación de hello e intercambio de claves criptográficas del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-124">Create an endpoint using Azure Active Directory for handling hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="3f5ff-125">Hola `--home-page` y `--identifier-uris` no es necesario toobe para direcciones enrutables real.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-125">hello `--home-page` and `--identifier-uris` do not need toobe actual routable address.</span></span> <span data-ttu-id="3f5ff-126">Hola más alto nivel de seguridad, los secretos de cliente deben utilizarse en lugar de contraseñas.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-126">For hello highest level of security, client secrets should be used instead of passwords.</span></span> <span data-ttu-id="3f5ff-127">Hola CLI de Azure actualmente no puede generar los secretos de cliente.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-127">hello Azure CLI cannot currently generate client secrets.</span></span> <span data-ttu-id="3f5ff-128">Los secretos de cliente sólo pueden generarse en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-128">Client secrets can only be generated in hello Azure portal.</span></span> <span data-ttu-id="3f5ff-129">Hello en el ejemplo siguiente se crea un extremo de Azure Active Directory denominado `myAADApp` y utiliza una contraseña de `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-129">hello following example creates an Azure Active Directory endpoint named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="3f5ff-130">Especifique su propia contraseña del siguiente modo:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-130">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="3f5ff-131">Hola Nota `applicationId` se muestra en la salida de hello de hello anterior comando.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-131">Note hello `applicationId` shown in hello output from hello preceding command.</span></span> <span data-ttu-id="3f5ff-132">Este identificador de la aplicación se utiliza en hello pasos:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-132">This application ID is used in hello following steps:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

<span data-ttu-id="3f5ff-133">Agregue un tooan de disco de datos existente de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-133">Add a data disk tooan existing VM.</span></span> <span data-ttu-id="3f5ff-134">Hello en el ejemplo siguiente se agrega un tooa de disco de datos máquina virtual denominada `myVM`:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-134">hello following example adds a data disk tooa VM named `myVM`:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="3f5ff-135">Revise los detalles de Hola para su clave de hello y el almacén de claves que creó.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-135">Review hello details for your Key Vault and hello key you created.</span></span> <span data-ttu-id="3f5ff-136">Necesita Hola identificador de almacén de claves, URI y clave de dirección URL en el paso final de Hola.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-136">You need hello Key Vault ID, URI, and key URL in hello final step.</span></span> <span data-ttu-id="3f5ff-137">Hello en el ejemplo siguiente se revisa Hola detalles para un almacén de claves denominado `myKeyVault` y clave denominada `myKey`:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-137">hello following example reviews hello details for a Key Vault named `myKeyVault` and key named `myKey`:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="3f5ff-138">Cifre los discos como se indica a continuación, con sus propios parámetros:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-138">Encrypt your disks as follows, entering your own parameter names throughout:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="3f5ff-139">Hola CLI de Azure no proporciona errores detallados durante el proceso de cifrado de Hola.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-139">hello Azure CLI doesn't provide verbose errors during hello encryption process.</span></span> <span data-ttu-id="3f5ff-140">Para obtener información adicional para la solución de problemas, consulte `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-140">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span></span> <span data-ttu-id="3f5ff-141">Como Hola anterior comando tiene muchas variables y es posible que no obtenga mucho indicación como toowhy Hola proceso se produce un error, un ejemplo de comando completo sería como sigue:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-141">As hello preceding command has many variables and you may not get much indication as toowhy hello process fails, a complete command example would be as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

<span data-ttu-id="3f5ff-142">Por último, revise el estado de cifrado de hello nuevo tooconfirm que los discos virtuales ahora se han cifrado.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-142">Finally, review hello encryption status again tooconfirm that your virtual disks have now been encrypted.</span></span> <span data-ttu-id="3f5ff-143">Hello en el ejemplo siguiente se comprueba estado Hola de una máquina virtual denominada `myVM` en hello `myResourceGroup` grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-143">hello following example checks hello status of a VM named `myVM` in hello `myResourceGroup` resource group:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="3f5ff-144">Introducción al cifrado de discos</span><span class="sxs-lookup"><span data-stu-id="3f5ff-144">Overview of disk encryption</span></span>
<span data-ttu-id="3f5ff-145">Los discos virtuales en máquinas virtuales Linux se cifran en reposo mediante [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="3f5ff-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="3f5ff-146">El cifrado de los discos virtuales en Azure no conlleva ningún cargo.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="3f5ff-147">Las claves criptográficas se almacenan en el almacén de claves de Azure mediante la protección de software, o puede importar o generar las claves en módulos de seguridad de Hardware (HSM) de certificados tooFIPS estándares de 140-2 nivel 2.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="3f5ff-148">Estas claves criptográficas se pueden controlar y se puede auditar su uso.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="3f5ff-149">Estas claves criptográficas son tooencrypt usado y descifrar los discos virtuales conectados tooyour máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-149">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="3f5ff-150">Como las máquinas virtuales se encienden y se apagan, los puntos de conexión de Azure Active Directory ofrecen un mecanismo seguro para la emisión de estas claves criptográficas.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-150">An Azure Active Directory endpoint provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="3f5ff-151">proceso de Hola para cifrar una máquina virtual es como sigue:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-151">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="3f5ff-152">Cree una clave criptográfica en Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="3f5ff-153">Configurar el número de toobe criptográficos clave de hello utilizable para el cifrado de discos.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-153">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="3f5ff-154">clave criptográfica de hello tooread de hello almacén de claves de Azure, cree un punto de conexión con Azure Active Directory con los permisos adecuados de Hola.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-154">tooread hello cryptographic key from hello Azure Key Vault, create an endpoint using Azure Active Directory with hello appropriate permissions.</span></span>
4. <span data-ttu-id="3f5ff-155">Emitir Hola comando tooencrypt los discos virtuales, especificar el punto de conexión de hello Azure Active Directory y adecuado toobe clave criptográfico utilizado.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-155">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory endpoint and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="3f5ff-156">extremo de Azure Active Directory de Hello las solicitudes de clave de cifrado necesario Hola desde el almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-156">hello Azure Active Directory endpoint requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="3f5ff-157">discos virtuales de Hola se cifran mediante la clave criptográfica de hello proporcionado.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-157">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="supporting-services-and-encryption-process"></a><span data-ttu-id="3f5ff-158">Servicios de soporte y proceso de cifrado</span><span class="sxs-lookup"><span data-stu-id="3f5ff-158">Supporting services and encryption process</span></span>
<span data-ttu-id="3f5ff-159">Cifrado del disco se basa en hello adicionales de los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-159">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="3f5ff-160">**Almacén de claves de Azure** -utilizar claves criptográficas toosafeguard y secretos usados para el proceso de cifrado y descifrado de hello del disco.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-160">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span>
  * <span data-ttu-id="3f5ff-161">Si ya existe un almacén de Azure Key Vault, puede utilizarlo.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="3f5ff-162">No es necesario toodedicate los discos de tooencrypting de almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-162">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="3f5ff-163">límites administrativos tooseparate y visibilidad de clave, puede crear un almacén de claves dedicado.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-163">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="3f5ff-164">**Azure Active Directory** : Hola de identificadores de intercambio seguro de claves cifradas necesarias y autenticación para solicitado acciones.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-164">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="3f5ff-165">Normalmente, puede usar un almacén existente de Azure Active Directory para hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="3f5ff-166">aplicación Hello es más de un punto de conexión para el almacén de claves de Hola y toorequest de servicios de máquina Virtual y obtener emitido claves criptográficas de hello adecuado.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-166">hello application is more of an endpoint for hello Key Vault and Virtual Machine services toorequest and get issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="3f5ff-167">No está desarrollando una aplicación real que se integrará con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="3f5ff-168">Requisitos y limitaciones</span><span class="sxs-lookup"><span data-stu-id="3f5ff-168">Requirements and limitations</span></span>
<span data-ttu-id="3f5ff-169">Requisitos y escenarios admitidos para el cifrado de discos:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="3f5ff-170">Hola después de servidor Linux SKU - Ubuntu, CentOS, SUSE y SUSE Linux Enterprise Server (SLES) y Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-170">hello following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="3f5ff-171">Todos los recursos (por ejemplo, el almacén de claves, la cuenta de almacenamiento y VM) deben estar en hello misma región de Azure y la suscripción.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-171">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="3f5ff-172">Máquinas virtuales estándar de las series A, D, DS, G y GS.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="3f5ff-173">Cifrado del disco no se admite actualmente en hello los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-173">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="3f5ff-174">Máquina s virtuales de nivel básico</span><span class="sxs-lookup"><span data-stu-id="3f5ff-174">Basic tier VMs.</span></span>
* <span data-ttu-id="3f5ff-175">Máquinas virtuales creadas mediante el modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-175">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="3f5ff-176">Deshabilitado del cifrado de disco de sistema operativo en máquinas virtuales Linux.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="3f5ff-177">Actualizar las claves criptográficas de hello en una VM de Linux ya se ha cifrado.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-177">Updating hello cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-hello-azure-key-vault-and-keys"></a><span data-ttu-id="3f5ff-178">Crear Hola almacén de claves de Azure y claves</span><span class="sxs-lookup"><span data-stu-id="3f5ff-178">Create hello Azure Key Vault and keys</span></span>
<span data-ttu-id="3f5ff-179">resto de hello toocomplete de esta guía, debe hello [más reciente 1.0 de CLI de Azure](../../xplat-cli-install.md) instalado e inició sesión mediante el modo de administrador de recursos de hello como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-179">toocomplete hello remainder of this guide, you need hello [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="3f5ff-180">A lo largo de los ejemplos de comandos de hello, reemplace todos los parámetros de ejemplo con sus propios nombres, la ubicación y los valores de clave.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-180">Throughout hello command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="3f5ff-181">Hello en los ejemplos siguientes utilizan una convención de `myResourceGroup`, `myKeyVault`, `myAADApp`, etcetera.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-181">hello following examples use a convention of `myResourceGroup`, `myKeyVault`, `myAADApp`, etc.</span></span>

<span data-ttu-id="3f5ff-182">primer paso de Hello es un almacén de claves de Azure toostore toocreate las claves criptográficas.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-182">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="3f5ff-183">Almacén de claves de Azure puede almacenar secretos, claves o contraseñas que permiten toosecurely implementan en sus aplicaciones y servicios.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-183">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="3f5ff-184">Para el cifrado de disco virtual, utilice toostore de almacén de claves una clave criptográfica que es usado tooencrypt o descifrar los discos virtuales.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-184">For virtual disk encryption, you use Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="3f5ff-185">Habilitar el proveedor de almacén de claves de Azure de hello en su suscripción de Azure, a continuación, crear un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-185">Enable hello Azure Key Vault provider in your Azure subscription, then create a resource group.</span></span> <span data-ttu-id="3f5ff-186">Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `WestUS` ubicación:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-186">hello following example creates a resource group named `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="3f5ff-187">Hola almacén de claves de Azure que lo contiene hello las claves criptográfico y proceso asociado recursos como almacenamiento y Hola propia máquina virtual deben residir en Hola misma región.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-187">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="3f5ff-188">Hello en el ejemplo siguiente se crea un almacén de claves de Azure denominado `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-188">hello following example creates an Azure Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="3f5ff-189">Puede almacenar las claves criptográficas mediante software o protección del modelo de seguridad de hardware (HSM).</span><span class="sxs-lookup"><span data-stu-id="3f5ff-189">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="3f5ff-190">Para usar HSM se necesita un almacén premium de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-190">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="3f5ff-191">Hay un costo adicional toocreating una prima el almacén de claves en lugar de almacén de claves estándar que almacena las claves protegidas por software.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-191">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="3f5ff-192">toocreate agregar un almacén de claves, premium Hola anterior paso `--sku Premium` toohello comando.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-192">toocreate a premium Key Vault, in hello preceding step add `--sku Premium` toohello command.</span></span> <span data-ttu-id="3f5ff-193">Hello en el ejemplo siguiente se usa claves protegidas por software ya que hemos creado un almacén de claves estándar.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-193">hello following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="3f5ff-194">Para los dos modelos de protección, Hola plataforma Windows Azure debe toobe concede acceso toorequest hello las claves criptográficas cuando Hola VM arranca discos virtuales de toodecrypt Hola.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-194">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="3f5ff-195">Cree una clave de cifrado en su almacén de Key Vault y habilítela para el cifrado de discos virtuales.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-195">Create an encryption key within your Key Vault, then enable it for use with virtual disk encryption.</span></span> <span data-ttu-id="3f5ff-196">Hello en el ejemplo siguiente se crea una clave denominada `myKey` y, a continuación, se habilita para el cifrado de disco:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-196">hello following example creates a key named `myKey` and then enables it for disk encryption:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-hello-azure-active-directory-application"></a><span data-ttu-id="3f5ff-197">Crear aplicación de Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="3f5ff-197">Create hello Azure Active Directory application</span></span>
<span data-ttu-id="3f5ff-198">Cuando los discos virtuales se cifrada o descifrados, utilice una autenticación de hello toohandle de punto de conexión e intercambio de claves criptográficas del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-198">When virtual disks are encrypted or decrypted, you use an endpoint toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="3f5ff-199">Este punto de conexión, una aplicación de Azure Active Directory permite toorequest de la plataforma Windows Azure de Hola Hola adecuada las claves criptográficas en nombre de VM de Hola.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-199">This endpoint, an Azure Active Directory application, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="3f5ff-200">Su suscripción dispone de una instancia de Azure Active Directory predeterminada, aunque muchas organizaciones tienen directorios de Azure Active Directory dedicados.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-200">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="3f5ff-201">Como no está creando una aplicación de Azure Active Directory completa, Hola `--home-page` y `--identifier-uris` parámetros en el siguiente ejemplo de Hola no es necesario toobe para direcciones enrutables real.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-201">As you are not creating a full Azure Active Directory application, hello `--home-page` and `--identifier-uris` parameters in hello following example do not need toobe actual routable address.</span></span> <span data-ttu-id="3f5ff-202">Hello siguiente ejemplo también especifica un secreto basado en contraseña, en lugar de generar claves desde dentro de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-202">hello following example also specifies a password-based secret rather than generating keys from within hello Azure portal.</span></span> <span data-ttu-id="3f5ff-203">En este momento, la generación de claves no puede realizarse desde Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-203">As this time, generating keys cannot be done from hello Azure CLI.</span></span>

<span data-ttu-id="3f5ff-204">Cree una aplicación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-204">Create your Azure Active Directory application.</span></span> <span data-ttu-id="3f5ff-205">Hello en el ejemplo siguiente se crea una aplicación denominada `myAADApp` y utiliza una contraseña de `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-205">hello following example creates an application named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="3f5ff-206">Especifique su propia contraseña del siguiente modo:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-206">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="3f5ff-207">Tome nota de hello `applicationId` que se devuelve en la salida de hello de hello anterior comando.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-207">Make a note of hello `applicationId` that is returned in hello output from hello preceding command.</span></span> <span data-ttu-id="3f5ff-208">Este identificador de la aplicación se utiliza en algunos Hola restantes pasos.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-208">This application ID is used in some of hello remaining steps.</span></span> <span data-ttu-id="3f5ff-209">A continuación, cree un nombre principal de servicio (SPN) para que la aplicación hello es accesible dentro de su entorno.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-209">Next, create a service principal name (SPN) so that hello application is accessible within your environment.</span></span> <span data-ttu-id="3f5ff-210">toosuccessfully cifrar o descifrar los discos virtuales, permisos de clave cifrado de hello almacenados en el almacén de claves deben ser conjunto toopermit hello Azure Active Directory aplicación tooread Hola claves.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-210">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory application tooread hello keys.</span></span>

<span data-ttu-id="3f5ff-211">Cree Hola SPN y establezca los permisos adecuados de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-211">Create hello SPN and set hello appropriate permissions as follows:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a><span data-ttu-id="3f5ff-212">Incorporación de un disco virtual y revisión del estado del cifrado</span><span class="sxs-lookup"><span data-stu-id="3f5ff-212">Add a virtual disk and review encryption status</span></span>
<span data-ttu-id="3f5ff-213">tooactually cifrar algunos discos virtuales, permite agregar un tooan de disco existente de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-213">tooactually encrypt some virtual disks, lets add a disk tooan existing VM.</span></span> <span data-ttu-id="3f5ff-214">Agregue un tooan de disco de datos de 5Gb existente VM como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-214">Add a 5Gb data disk tooan existing VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="3f5ff-215">discos virtuales de Hello no se cifran actualmente.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-215">hello virtual disks are not currently encrypted.</span></span> <span data-ttu-id="3f5ff-216">Revisar estado de cifrado actual de hello de la máquina virtual como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-216">Review hello current encryption status of your VM as follows:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a><span data-ttu-id="3f5ff-217">Cifrado de discos virtuales</span><span class="sxs-lookup"><span data-stu-id="3f5ff-217">Encrypt virtual disks</span></span>
<span data-ttu-id="3f5ff-218">toonow cifrar discos virtuales hello, reunir todos los componentes anteriores de hello:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-218">toonow encrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="3f5ff-219">Especifique la contraseña y la aplicación de Azure Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-219">Specify hello Azure Active Directory application and password.</span></span>
2. <span data-ttu-id="3f5ff-220">Especificar Hola el almacén de claves toostore Hola metadatos para los discos cifrados.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-220">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="3f5ff-221">Especifique hello toouse de claves criptográficas para hello real cifrado y descifrado.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-221">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="3f5ff-222">Especifique si desea que tooencrypt disco de SO hello, discos de datos de Hola o todos.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-222">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="3f5ff-223">Permite revisar los detalles de Hola para su clave de hello y el almacén de claves de Azure que creó, imprescindible Hola identificador de almacén de claves, URI, y, a continuación, dirección URL de claves en el paso final de hello:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-223">Lets review hello details for your Azure Key Vault and hello key you created, as you need hello Key Vault ID, URI, and then key URL in hello final step:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="3f5ff-224">Cifrar los discos virtuales con valores obtenidos hello en hello `azure keyvault show` y `azure keyvault key show` comandos como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-224">Encrypt your virtual disks using hello output from hello `azure keyvault show` and `azure keyvault key show` commands as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="3f5ff-225">Como hello comando anterior tiene muchas variables, hello en el ejemplo siguiente se es comando completo de hello como referencia:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-225">As hello preceding command has many variables, hello following example is hello complete command for reference:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

<span data-ttu-id="3f5ff-226">Hola CLI de Azure no proporciona errores detallados durante el proceso de cifrado de Hola.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-226">hello Azure CLI doesn't provide verbose errors during hello encryption process.</span></span> <span data-ttu-id="3f5ff-227">Para obtener información adicional sobre solución de problemas, revise `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` en hello VM que se va a cifrar.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-227">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` on hello VM you are encrypting.</span></span>

<span data-ttu-id="3f5ff-228">Por último, permite revisar el estado de cifrado de hello nuevo tooconfirm que los discos virtuales ahora se han cifrado:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-228">Finally, lets review hello encryption status again tooconfirm that your virtual disks have now been encrypted:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a><span data-ttu-id="3f5ff-229">Adición de discos de datos adicionales</span><span class="sxs-lookup"><span data-stu-id="3f5ff-229">Add additional data disks</span></span>
<span data-ttu-id="3f5ff-230">Una vez que haya cifrado los discos de datos, puede agregar más adelante discos virtuales adicionales tooyour VM y cifrarlas también.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-230">Once you have encrypted your data disks, you can later add additional virtual disks tooyour VM and also encrypt them.</span></span> <span data-ttu-id="3f5ff-231">Cuando ejecute hello `azure vm enable-disk-encryption` comando, la versión de la secuencia de hello incremento con hello `--sequence-version` parámetro.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-231">When you run hello `azure vm enable-disk-encryption` command, increment hello sequence version using hello `--sequence-version` parameter.</span></span> <span data-ttu-id="3f5ff-232">Este parámetro de versión de secuencia permite tooperform sucesivas operaciones efectuadas sobre Hola misma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3f5ff-232">This sequence version parameter allows you tooperform repeated operations on hello same VM.</span></span>

<span data-ttu-id="3f5ff-233">Por ejemplo, permite agregar un segundo tooyour de disco virtual VM como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-233">For example, lets add a second virtual disk tooyour VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="3f5ff-234">Vuelva a ejecutar Hola comando tooencrypt Hola discos virtuales, esta vez agrega hello `--sequence-version` parámetro y Hola valor incremental de nuestro primer ejecutar como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="3f5ff-234">Rerun hello command tooencrypt hello virtual disks, this time adding hello `--sequence-version` parameter, and incrementing hello value from our first run as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
  --sequence-version 2
```


## <a name="next-steps"></a><span data-ttu-id="3f5ff-235">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3f5ff-235">Next steps</span></span>
* <span data-ttu-id="3f5ff-236">Para más información acerca de cómo administrar Azure Key Vault, incluido cómo eliminar claves criptográficas y almacenes, consulte [Administración de Key Vault mediante CLI](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="3f5ff-236">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="3f5ff-237">Para obtener más información acerca del cifrado de disco, como preparar una tooAzure tooupload personalizado cifrado de VM, consulte [cifrado del disco de Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="3f5ff-237">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
