---
title: aaaJoin un tooan RedHat Linux VM Azure Active Directory DS | Documentos de Microsoft
description: "¿Cómo toojoin un tooan RedHat Enterprise Linux 7 VM existente servicio del dominio de Active Directory de Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/14/2016
ms.author: v-livech
ms.openlocfilehash: f3ba3c764e253191753f1cc5fc8c3b85c53818af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-redhat-linux-vm-tooan-azure-active-directory-domain-service"></a><span data-ttu-id="33b54-103">Unirse a un servicio del dominio de Active Directory de Azure de RedHat Linux VM tooan</span><span class="sxs-lookup"><span data-stu-id="33b54-103">Join a RedHat Linux VM tooan Azure Active Directory Domain Service</span></span>

<span data-ttu-id="33b54-104">Este artículo muestra cómo toojoin una tooan de máquina virtual de Red Hat Enterprise Linux (RHEL) 7 Servicios de dominio de Active Directory (AADDS) de Azure administra el dominio.</span><span class="sxs-lookup"><span data-stu-id="33b54-104">This article shows you how toojoin a Red Hat Enterprise Linux (RHEL) 7 virtual machine tooan Azure Active Directory Domain Services (AADDS) managed domain.</span></span>  <span data-ttu-id="33b54-105">Hola requisitos son:</span><span class="sxs-lookup"><span data-stu-id="33b54-105">hello requirements are:</span></span>

- <span data-ttu-id="33b54-106">[una cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/);</span><span class="sxs-lookup"><span data-stu-id="33b54-106">[an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>

- <span data-ttu-id="33b54-107">[archivos de clave SSH pública y privada](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="33b54-107">[SSH public and private key files](mac-create-ssh-keys.md)</span></span>

- [<span data-ttu-id="33b54-108">un controlador de dominio de Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="33b54-108">an Azure Active Directory Domain Services DC</span></span>](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="33b54-109">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="33b54-109">Quick Commands</span></span>

<span data-ttu-id="33b54-110">_Reemplace los ejemplos por su propia configuración._</span><span class="sxs-lookup"><span data-stu-id="33b54-110">_Replace any examples with your own settings._</span></span>

### <a name="switch-hello-azure-cli-tooclassic-deployment-mode"></a><span data-ttu-id="33b54-111">Cambiar el modo de implementación de tooclassic Hola cli de azure</span><span class="sxs-lookup"><span data-stu-id="33b54-111">Switch hello azure-cli tooclassic deployment mode</span></span>

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a><span data-ttu-id="33b54-112">Buscar una imagen y versión de RHEL</span><span class="sxs-lookup"><span data-stu-id="33b54-112">Search for a RHEL version and image</span></span>

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a><span data-ttu-id="33b54-113">Crear una máquina virtual de Redhat Linux</span><span class="sxs-lookup"><span data-stu-id="33b54-113">Create a Redhat Linux VM</span></span>

```azurecli
azure vm create myVM \
-o a879bbefc56a43abb0ce65052aac09f3__RHEL_7_2_Standard_Azure_RHUI-20161026220742 \
-g ahmet \
-p myPassword \
-e 22 \
-t "~/.ssh/id_rsa.pub" \
-z "Small" \
-l "West US"
```

### <a name="ssh-toohello-vm"></a><span data-ttu-id="33b54-114">SSH toohello VM</span><span class="sxs-lookup"><span data-stu-id="33b54-114">SSH toohello VM</span></span>

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a><span data-ttu-id="33b54-115">Actualizar paquetes YUM</span><span class="sxs-lookup"><span data-stu-id="33b54-115">Update YUM packages</span></span>

```bash
sudo yum update
```

### <a name="install-packages-needed"></a><span data-ttu-id="33b54-116">Instalar los paquetes necesarios</span><span class="sxs-lookup"><span data-stu-id="33b54-116">Install packages needed</span></span>

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

<span data-ttu-id="33b54-117">Ahora que los paquetes de saludo necesario están instalados en la máquina virtual de Linux de hello, Hola siguiente tarea es dominio administrado del toohello toojoin Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="33b54-117">Now that hello required packages are installed on hello Linux virtual machine, hello next task is toojoin hello virtual machine toohello managed domain.</span></span>

### <a name="discover-hello-aad-domain-services-managed-domain"></a><span data-ttu-id="33b54-118">Detectar el dominio administrado de los servicios de dominio de AAD de Hola</span><span class="sxs-lookup"><span data-stu-id="33b54-118">Discover hello AAD Domain Services managed domain</span></span>

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a><span data-ttu-id="33b54-119">Inicializar kerberos</span><span class="sxs-lookup"><span data-stu-id="33b54-119">Initialize kerberos</span></span>

<span data-ttu-id="33b54-120">Asegúrese de especificar un usuario que pertenece el grupo toohello 'AAD DC administradores'.</span><span class="sxs-lookup"><span data-stu-id="33b54-120">Ensure that you specify a user who belongs toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="33b54-121">Solo estos usuarios pueden unirse a dominio administrado de equipos toohello.</span><span class="sxs-lookup"><span data-stu-id="33b54-121">Only these users can join computers toohello managed domain.</span></span>

```bash
kinit ahmet@mydomain.com
```

### <a name="join-hello-machine-toohello-domain"></a><span data-ttu-id="33b54-122">Unirse a dominio de hello máquina toohello</span><span class="sxs-lookup"><span data-stu-id="33b54-122">Join hello machine toohello domain</span></span>

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-hello-machine-is-joined-toohello-domain"></a><span data-ttu-id="33b54-123">Compruebe la máquina de hello es toohello Unidos a un dominio</span><span class="sxs-lookup"><span data-stu-id="33b54-123">Verify hello machine is joined toohello domain</span></span>

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="33b54-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="33b54-124">Next Steps</span></span>

* [<span data-ttu-id="33b54-125">Red Hat Update Infrastructure (RHUI) para máquinas virtuales Red Hat Enterprise Linux a petición en Azure</span><span class="sxs-lookup"><span data-stu-id="33b54-125">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="33b54-126">Configuración de una instancia de Key Vault para máquinas virtuales en Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="33b54-126">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="33b54-127">Implementar y administrar máquinas virtuales usando plantillas del Administrador de recursos de Azure y Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="33b54-127">Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI</span></span>](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
