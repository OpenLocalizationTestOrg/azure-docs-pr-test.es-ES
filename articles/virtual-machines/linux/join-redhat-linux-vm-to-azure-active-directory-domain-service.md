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
# <a name="join-a-redhat-linux-vm-tooan-azure-active-directory-domain-service"></a>Unirse a un servicio del dominio de Active Directory de Azure de RedHat Linux VM tooan

Este artículo muestra cómo toojoin una tooan de máquina virtual de Red Hat Enterprise Linux (RHEL) 7 Servicios de dominio de Active Directory (AADDS) de Azure administra el dominio.  Hola requisitos son:

- [una cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/);

- [archivos de clave SSH pública y privada](mac-create-ssh-keys.md).

- [un controlador de dominio de Azure Active Directory Domain Services](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a>Comandos rápidos

_Reemplace los ejemplos por su propia configuración._

### <a name="switch-hello-azure-cli-tooclassic-deployment-mode"></a>Cambiar el modo de implementación de tooclassic Hola cli de azure

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a>Buscar una imagen y versión de RHEL

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a>Crear una máquina virtual de Redhat Linux

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

### <a name="ssh-toohello-vm"></a>SSH toohello VM

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a>Actualizar paquetes YUM

```bash
sudo yum update
```

### <a name="install-packages-needed"></a>Instalar los paquetes necesarios

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

Ahora que los paquetes de saludo necesario están instalados en la máquina virtual de Linux de hello, Hola siguiente tarea es dominio administrado del toohello toojoin Hola máquina virtual.

### <a name="discover-hello-aad-domain-services-managed-domain"></a>Detectar el dominio administrado de los servicios de dominio de AAD de Hola

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a>Inicializar kerberos

Asegúrese de especificar un usuario que pertenece el grupo toohello 'AAD DC administradores'. Solo estos usuarios pueden unirse a dominio administrado de equipos toohello.

```bash
kinit ahmet@mydomain.com
```

### <a name="join-hello-machine-toohello-domain"></a>Unirse a dominio de hello máquina toohello

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-hello-machine-is-joined-toohello-domain"></a>Compruebe la máquina de hello es toohello Unidos a un dominio

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a>Pasos siguientes

* [Red Hat Update Infrastructure (RHUI) para máquinas virtuales Red Hat Enterprise Linux a petición en Azure](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Configuración de una instancia de Key Vault para máquinas virtuales en Azure Resource Manager](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Implementar y administrar máquinas virtuales usando plantillas del Administrador de recursos de Azure y Hola CLI de Azure](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
