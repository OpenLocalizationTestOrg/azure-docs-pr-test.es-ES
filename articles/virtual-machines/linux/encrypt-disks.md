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
# <a name="how-tooencrypt-virtual-disks-on-a-linux-vm"></a>¿Cómo tooencrypt discos virtuales en una VM Linux
Para mejorar la seguridad y el cumplimiento de las máquinas virtuales, se pueden cifrar los discos virtuales en Azure. Los discos se cifran mediante claves criptográficas que están protegidas en Azure Key Vault. Estas claves criptográficas se pueden controlar y se puede auditar su uso. Este artículo detalla cómo tooencrypt discos virtuales en una VM de Linux con Hola 2.0 de CLI de Azure. También puede realizar estos pasos con hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-commands"></a>Comandos rápidos
Si necesita tooquickly realizar la tarea hello, Hola después Hola de detalles de la sección base comandos tooencrypt discos virtuales en la máquina virtual. Obtener más información y el contexto de cada paso se encuentran rest Hola de documento de hello, [a partir de aquí](#overview-of-disk-encryption).

Necesita hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login). En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores. Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *myKey* y *myVM*.

En primer lugar, habilitar el proveedor de almacén de claves de Azure de hello dentro de su suscripción de Azure con [registro de proveedor az](/cli/azure/provider#register) y crear un grupo de recursos con [crear grupo az](/cli/azure/group#create). Hello en el ejemplo siguiente se crea un nombre de grupo de recursos *myResourceGroup* en hello *eastus* ubicación:

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

Crear un almacén de claves de Azure con [crear az keyvault](/cli/azure/keyvault#create) y habilitar Hola el almacén de claves para su uso con el cifrado del disco. Especifique un nombre de Key Vault único para *keyvault_name* de la siguiente manera:

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

Cree una clave criptográfica en la instancia de Key Vault con [az keyvault key create](/cli/azure/keyvault/key#create). Hello en el ejemplo siguiente se crea una clave denominada *myKey*:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

Cree una entidad de servicio mediante Azure Active Directory con [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac). identificadores de entidad de seguridad de servicio de Hola Hola autenticación y el intercambio de claves criptográficas del almacén de claves. Hola de ejemplo siguiente lee en valores de hello para la entidad de servicio de hello identificador y la contraseña para su uso en los comandos posteriores:

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

contraseña de Hello solo se genera cuando creas Hola entidad de servicio. Si lo desea, ver y grabar Hola contraseña (`echo $sp_password`). Puede mostrar las entidades de servicio con el comando [az ad sp list](/cli/azure/ad/sp#list) y consultar información adicional sobre una entidad de servicio específica con [az ad sp show](/cli/azure/ad/sp#show).

Establezca permisos en Key Vault con [az keyvault set-policy](/cli/azure/keyvault#set-policy). En el siguiente ejemplo de Hola Hola Id. de entidad de seguridad de servicio proporcionado de hello anterior comando:

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

Cree una máquina virtual con [az vm create](/cli/azure/vm#create) y conecte un disco de datos de 5 GB. Solo ciertas imágenes de Marketplace admiten el cifrado de discos. Hello en el ejemplo siguiente se crea una máquina virtual denominada `myVM` con un **CentOS 7.2n** imagen:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

SSH tooyour VM con Hola `publicIpAddress` se muestra en la salida de hello de hello anterior comando. Crear una partición y un sistema de archivos y, a continuación, montar el disco de datos de Hola. Para obtener más información, consulte [conectar tooa nuevo disco de VM de Linux toomount hello](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk). Cierre la sesión de SSH.

Cifre la máquina virtual con [az vm encryption enable](/cli/azure/vm/encryption#enable). Hello en el ejemplo siguiente se usa hello `$sp_id` y `$sp_password` variables de hello anterior `ad sp create-for-rbac` comando:

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

Tarda algún tiempo para toocomplete de proceso de cifrado de disco Hola. Supervisar el estado de saludo del proceso de hello con [presentación con cifrado vm az](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Hola estado muestra **EncryptionInProgress**. Espere hasta que el estado de Hola Hola SO disco informes **VMRestartPending**, a continuación, reinicie la máquina virtual con [reinicio de la máquina virtual de az](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

proceso de cifrado de disco Hello se finaliza una durante el proceso de arranque de hello, por lo que espere unos minutos antes de comprobar el estado de Hola de nuevo con el cifrado **presentación con cifrado vm az**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

estado de Hello ahora debería notificar disco Hola sistema operativo y disco de datos como **Encrypted**.

## <a name="overview-of-disk-encryption"></a>Introducción al cifrado de discos
Los discos virtuales en máquinas virtuales Linux se cifran en reposo mediante [dm-crypt](https://wikipedia.org/wiki/Dm-crypt). El cifrado de los discos virtuales en Azure no conlleva ningún cargo. Las claves criptográficas se almacenan en el almacén de claves de Azure mediante la protección de software, o puede importar o generar las claves en módulos de seguridad de Hardware (HSM) de certificados tooFIPS estándares de 140-2 nivel 2. Estas claves criptográficas se pueden controlar y se puede auditar su uso. Estas claves criptográficas son tooencrypt usado y descifrar los discos virtuales conectados tooyour máquina virtual. Como las máquinas virtuales se encienden y se apagan, una entidad de servicio de Azure Active Directory proporciona un mecanismos seguro para la emisión de estas claves criptográficas.

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

* Hola después de servidor Linux SKU - Ubuntu, CentOS, SUSE y SUSE Linux Enterprise Server (SLES) y Red Hat Enterprise Linux.
* Todos los recursos (por ejemplo, el almacén de claves, la cuenta de almacenamiento y VM) deben estar en hello misma región de Azure y la suscripción.
* Máquinas virtuales estándar de las series A, D, DS, G y GS.

Cifrado del disco no se admite actualmente en hello los escenarios siguientes:

* Máquina s virtuales de nivel básico
* Máquinas virtuales creadas mediante el modelo de implementación de hello clásico.
* Deshabilitado del cifrado de disco de sistema operativo en máquinas virtuales Linux.
* Actualizar las claves criptográficas de hello en una VM de Linux ya se ha cifrado.

## <a name="create-azure-key-vault-and-keys"></a>Creación de Azure Key Vault y claves
Necesita hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login). En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores. Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *myKey* y *myVM*.

primer paso de Hello es un almacén de claves de Azure toostore toocreate las claves criptográficas. Almacén de claves de Azure puede almacenar secretos, claves o contraseñas que permiten toosecurely implementan en sus aplicaciones y servicios. Para el cifrado de disco virtual, utilice toostore de almacén de claves una clave criptográfica que es usado tooencrypt o descifrar los discos virtuales.

Habilitar el proveedor de almacén de claves de Azure de hello dentro de su suscripción de Azure con [registro de proveedor az](/cli/azure/provider#register) y crear un grupo de recursos con [crear grupo az](/cli/azure/group#create). Hello en el ejemplo siguiente se crea un nombre de grupo de recursos *myResourceGroup* en hello `eastus` ubicación:

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

Hola almacén de claves de Azure que lo contiene hello las claves criptográfico y proceso asociado recursos como almacenamiento y Hola propia máquina virtual deben residir en Hola misma región. Crear un almacén de claves de Azure con [crear az keyvault](/cli/azure/keyvault#create) y habilitar Hola el almacén de claves para su uso con el cifrado del disco. Especifique un nombre de Key Vault único para *keyvault_name* de la siguiente manera:

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

Puede almacenar las claves criptográficas mediante software o protección del modelo de seguridad de hardware (HSM). Para usar HSM se necesita un almacén premium de Key Vault. Hay un costo adicional toocreating una prima el almacén de claves en lugar de almacén de claves estándar que almacena las claves protegidas por software. toocreate agregar un almacén de claves, premium Hola anterior paso `--sku Premium` toohello comando. Hello en el ejemplo siguiente se usa claves protegidas por software ya que hemos creado un almacén de claves estándar.

Para los dos modelos de protección, Hola plataforma Windows Azure debe toobe concede acceso toorequest hello las claves criptográficas cuando Hola VM arranca discos virtuales de toodecrypt Hola. Cree una clave criptográfica en la instancia de Key Vault con [az keyvault key create](/cli/azure/keyvault/key#create). Hello en el ejemplo siguiente se crea una clave denominada *myKey*:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-hello-azure-active-directory-service-principal"></a>Crear Hola entidad de servicio de Azure Active Directory
Cuando los discos virtuales se cifrada o descifrados, especifique una autenticación de cuentas de hello toohandle e intercambio de claves criptográficas del almacén de claves. Esta cuenta, una entidad de seguridad de servicio de Active Directory de Azure, permite toorequest de la plataforma Windows Azure de Hola Hola adecuada las claves criptográficas en nombre de VM de Hola. Su suscripción dispone de una instancia de Azure Active Directory predeterminada, aunque muchas organizaciones tienen directorios de Azure Active Directory dedicados.

Cree una entidad de servicio mediante Azure Active Directory con [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac). Hola de ejemplo siguiente lee en valores de hello para la entidad de servicio de hello identificador y la contraseña para su uso en los comandos posteriores:

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

contraseña de Hello solo se muestra cuando se crea el servicio de hello principal. Si lo desea, ver y grabar Hola contraseña (`echo $sp_password`). Puede mostrar las entidades de servicio con el comando [az ad sp list](/cli/azure/ad/sp#list) y consultar información adicional sobre una entidad de servicio específica con [az ad sp show](/cli/azure/ad/sp#show).

toosuccessfully cifrar o descifrar los discos virtuales, permisos de clave cifrado de hello almacenados en el almacén de claves deben ser conjunto toopermit hello Azure Active Directory service principal tooread Hola claves. Establezca permisos en Key Vault con [az keyvault set-policy](/cli/azure/keyvault#set-policy). En el siguiente ejemplo de Hola Hola Id. de entidad de seguridad de servicio proporcionado de hello anterior comando:

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a>Create virtual machine
tooactually cifrar algunos discos virtuales, permite crear una máquina virtual y agregar un disco de datos. Crear un tooencrypt VM con [crear vm az](/cli/azure/vm#create) y adjuntar un disco de datos de 5 Gb. Solo ciertas imágenes de Marketplace admiten el cifrado de discos. Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVM* con un **CentOS 7.2n** imagen:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

SSH tooyour VM con Hola `publicIpAddress` se muestra en la salida de hello de hello anterior comando. Crear una partición y un sistema de archivos y, a continuación, montar el disco de datos de Hola. Para obtener más información, consulte [conectar tooa nuevo disco de VM de Linux toomount hello](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk). Cierre la sesión de SSH.


## <a name="encrypt-virtual-machine"></a>Cifrado de máquina virtual
discos virtuales de tooencrypt hello, reúne todos los componentes anteriores de hello:

1. Especificar Hola entidad de servicio de Azure Active Directory y una contraseña.
2. Especificar Hola el almacén de claves toostore Hola metadatos para los discos cifrados.
3. Especifique hello toouse de claves criptográficas para hello real cifrado y descifrado.
4. Especifique si desea que tooencrypt disco de SO hello, discos de datos de Hola o todos.

Cifre la máquina virtual con [az vm encryption enable](/cli/azure/vm/encryption#enable). Hello en el ejemplo siguiente se usa hello `$sp_id` y `$sp_password` variables de hello anterior `ad sp create-for-rbac` comando:

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

Tarda algún tiempo para toocomplete de proceso de cifrado de disco Hola. Supervisar el estado de saludo del proceso de hello con [presentación con cifrado vm az](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Hola de salida es similar toohello siguiente ejemplo truncada:

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

Espere hasta que el estado de Hola Hola SO disco informes **VMRestartPending**, a continuación, reinicie la máquina virtual con [reinicio de la máquina virtual de az](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

proceso de cifrado de disco Hello se finaliza una durante el proceso de arranque de hello, por lo que espere unos minutos antes de comprobar el estado de Hola de nuevo con el cifrado **presentación con cifrado vm az**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

estado de Hello ahora debería notificar disco Hola sistema operativo y disco de datos como **Encrypted**.


## <a name="add-additional-data-disks"></a>Adición de discos de datos adicionales
Una vez que haya cifrado los discos de datos, puede agregar más adelante discos virtuales adicionales tooyour VM y cifrarlas también. Por ejemplo, permite agregar un segundo tooyour de disco virtual VM como se indica a continuación:

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

Vuelva a ejecutar Hola comando tooencrypt Hola los discos virtuales como sigue:

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


## <a name="next-steps"></a>Pasos siguientes
* Para más información acerca de cómo administrar Azure Key Vault, incluido cómo eliminar claves criptográficas y almacenes, consulte [Administración de Key Vault mediante CLI](../../key-vault/key-vault-manage-with-cli2.md).
* Para obtener más información acerca del cifrado de disco, como preparar una tooAzure tooupload personalizado cifrado de VM, consulte [cifrado del disco de Azure](../../security/azure-security-disk-encryption.md).
