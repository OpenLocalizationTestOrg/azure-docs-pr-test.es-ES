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
# <a name="encrypt-disks-on-a-linux-vm-using-hello-azure-cli-10"></a>Cifrar discos en una VM de Linux con hello Azure CLI 1.0
Para mejorar la seguridad y el cumplimiento de las máquinas virtuales, los discos virtuales en Azure se pueden cifrar en reposo. Los discos se cifran mediante claves criptográficas que están protegidas en Azure Key Vault. Estas claves criptográficas se pueden controlar y se puede auditar su uso. Este artículo detalla cómo tooencrypt discos virtuales en una VM de Linux con Hola 1.0 de CLI de Azure y modelo de implementación del Administrador de recursos de Hola.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello
Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

- [Azure 1.0 de CLI](#quick-commands) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)
- [Azure 2.0 CLI](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola

## <a name="quick-commands"></a>Comandos rápidos
Si necesita tooquickly realizar la tarea hello, Hola después Hola de detalles de la sección base comandos tooencrypt discos virtuales en la máquina virtual. Obtener más información y el contexto de cada paso se encuentran rest Hola de documento de hello, [a partir de aquí](#overview-of-disk-encryption).

Necesita hello [más reciente 1.0 de CLI de Azure](../../xplat-cli-install.md) instalado e inició sesión mediante el modo de administrador de recursos de hello como sigue:

```azurecli
azure config mode arm
```

En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores. Los nombres de parámetros de ejemplo incluyen `myResourceGroup`, `myKeyVault` y `myVM`.

En primer lugar, habilitar el proveedor de almacén de claves de Azure de hello dentro de su suscripción de Azure y crear un grupo de recursos. Hello en el ejemplo siguiente se crea un nombre de grupo de recursos `myResourceGroup` en hello `WestUS` ubicación:

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

Cree un almacén de Azure Key Vault. Hello en el ejemplo siguiente se crea un almacén de claves denominado `myKeyVault`:

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

Cree una clave criptográfica en su almacén de Key Vault y habilítela para el cifrado de discos. Hello en el ejemplo siguiente se crea una clave denominada `myKey`:

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

Crear un punto de conexión con Azure Active Directory para controlar la autenticación de hello e intercambio de claves criptográficas del almacén de claves. Hola `--home-page` y `--identifier-uris` no es necesario toobe para direcciones enrutables real. Hola más alto nivel de seguridad, los secretos de cliente deben utilizarse en lugar de contraseñas. Hola CLI de Azure actualmente no puede generar los secretos de cliente. Los secretos de cliente sólo pueden generarse en hello portal de Azure. Hello en el ejemplo siguiente se crea un extremo de Azure Active Directory denominado `myAADApp` y utiliza una contraseña de `myPassword`. Especifique su propia contraseña del siguiente modo:

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

Hola Nota `applicationId` se muestra en la salida de hello de hello anterior comando. Este identificador de la aplicación se utiliza en hello pasos:

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

Agregue un tooan de disco de datos existente de la máquina virtual. Hello en el ejemplo siguiente se agrega un tooa de disco de datos máquina virtual denominada `myVM`:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

Revise los detalles de Hola para su clave de hello y el almacén de claves que creó. Necesita Hola identificador de almacén de claves, URI y clave de dirección URL en el paso final de Hola. Hello en el ejemplo siguiente se revisa Hola detalles para un almacén de claves denominado `myKeyVault` y clave denominada `myKey`:

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

Cifre los discos como se indica a continuación, con sus propios parámetros:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

Hola CLI de Azure no proporciona errores detallados durante el proceso de cifrado de Hola. Para obtener información adicional para la solución de problemas, consulte `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`. Como Hola anterior comando tiene muchas variables y es posible que no obtenga mucho indicación como toowhy Hola proceso se produce un error, un ejemplo de comando completo sería como sigue:

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

Por último, revise el estado de cifrado de hello nuevo tooconfirm que los discos virtuales ahora se han cifrado. Hello en el ejemplo siguiente se comprueba estado Hola de una máquina virtual denominada `myVM` en hello `myResourceGroup` grupo de recursos:

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a>Introducción al cifrado de discos
Los discos virtuales en máquinas virtuales Linux se cifran en reposo mediante [dm-crypt](https://wikipedia.org/wiki/Dm-crypt). El cifrado de los discos virtuales en Azure no conlleva ningún cargo. Las claves criptográficas se almacenan en el almacén de claves de Azure mediante la protección de software, o puede importar o generar las claves en módulos de seguridad de Hardware (HSM) de certificados tooFIPS estándares de 140-2 nivel 2. Estas claves criptográficas se pueden controlar y se puede auditar su uso. Estas claves criptográficas son tooencrypt usado y descifrar los discos virtuales conectados tooyour máquina virtual. Como las máquinas virtuales se encienden y se apagan, los puntos de conexión de Azure Active Directory ofrecen un mecanismo seguro para la emisión de estas claves criptográficas.

proceso de Hola para cifrar una máquina virtual es como sigue:

1. Cree una clave criptográfica en Azure Key Vault.
2. Configurar el número de toobe criptográficos clave de hello utilizable para el cifrado de discos.
3. clave criptográfica de hello tooread de hello almacén de claves de Azure, cree un punto de conexión con Azure Active Directory con los permisos adecuados de Hola.
4. Emitir Hola comando tooencrypt los discos virtuales, especificar el punto de conexión de hello Azure Active Directory y adecuado toobe clave criptográfico utilizado.
5. extremo de Azure Active Directory de Hello las solicitudes de clave de cifrado necesario Hola desde el almacén de claves de Azure.
6. discos virtuales de Hola se cifran mediante la clave criptográfica de hello proporcionado.

## <a name="supporting-services-and-encryption-process"></a>Servicios de soporte y proceso de cifrado
Cifrado del disco se basa en hello adicionales de los componentes siguientes:

* **Almacén de claves de Azure** -utilizar claves criptográficas toosafeguard y secretos usados para el proceso de cifrado y descifrado de hello del disco.
  * Si ya existe un almacén de Azure Key Vault, puede utilizarlo. No es necesario toodedicate los discos de tooencrypting de almacén de claves.
  * límites administrativos tooseparate y visibilidad de clave, puede crear un almacén de claves dedicado.
* **Azure Active Directory** : Hola de identificadores de intercambio seguro de claves cifradas necesarias y autenticación para solicitado acciones.
  * Normalmente, puede usar un almacén existente de Azure Active Directory para hospedar la aplicación.
  * aplicación Hello es más de un punto de conexión para el almacén de claves de Hola y toorequest de servicios de máquina Virtual y obtener emitido claves criptográficas de hello adecuado. No está desarrollando una aplicación real que se integrará con Azure Active Directory.

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

## <a name="create-hello-azure-key-vault-and-keys"></a>Crear Hola almacén de claves de Azure y claves
resto de hello toocomplete de esta guía, debe hello [más reciente 1.0 de CLI de Azure](../../xplat-cli-install.md) instalado e inició sesión mediante el modo de administrador de recursos de hello como se indica a continuación:

```azurecli
azure config mode arm
```

A lo largo de los ejemplos de comandos de hello, reemplace todos los parámetros de ejemplo con sus propios nombres, la ubicación y los valores de clave. Hello en los ejemplos siguientes utilizan una convención de `myResourceGroup`, `myKeyVault`, `myAADApp`, etcetera.

primer paso de Hello es un almacén de claves de Azure toostore toocreate las claves criptográficas. Almacén de claves de Azure puede almacenar secretos, claves o contraseñas que permiten toosecurely implementan en sus aplicaciones y servicios. Para el cifrado de disco virtual, utilice toostore de almacén de claves una clave criptográfica que es usado tooencrypt o descifrar los discos virtuales.

Habilitar el proveedor de almacén de claves de Azure de hello en su suscripción de Azure, a continuación, crear un grupo de recursos. Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `WestUS` ubicación:

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

Hola almacén de claves de Azure que lo contiene hello las claves criptográfico y proceso asociado recursos como almacenamiento y Hola propia máquina virtual deben residir en Hola misma región. Hello en el ejemplo siguiente se crea un almacén de claves de Azure denominado `myKeyVault`:

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

Puede almacenar las claves criptográficas mediante software o protección del modelo de seguridad de hardware (HSM). Para usar HSM se necesita un almacén premium de Key Vault. Hay un costo adicional toocreating una prima el almacén de claves en lugar de almacén de claves estándar que almacena las claves protegidas por software. toocreate agregar un almacén de claves, premium Hola anterior paso `--sku Premium` toohello comando. Hello en el ejemplo siguiente se usa claves protegidas por software ya que hemos creado un almacén de claves estándar.

Para los dos modelos de protección, Hola plataforma Windows Azure debe toobe concede acceso toorequest hello las claves criptográficas cuando Hola VM arranca discos virtuales de toodecrypt Hola. Cree una clave de cifrado en su almacén de Key Vault y habilítela para el cifrado de discos virtuales. Hello en el ejemplo siguiente se crea una clave denominada `myKey` y, a continuación, se habilita para el cifrado de disco:

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-hello-azure-active-directory-application"></a>Crear aplicación de Azure Active Directory hello
Cuando los discos virtuales se cifrada o descifrados, utilice una autenticación de hello toohandle de punto de conexión e intercambio de claves criptográficas del almacén de claves. Este punto de conexión, una aplicación de Azure Active Directory permite toorequest de la plataforma Windows Azure de Hola Hola adecuada las claves criptográficas en nombre de VM de Hola. Su suscripción dispone de una instancia de Azure Active Directory predeterminada, aunque muchas organizaciones tienen directorios de Azure Active Directory dedicados.

Como no está creando una aplicación de Azure Active Directory completa, Hola `--home-page` y `--identifier-uris` parámetros en el siguiente ejemplo de Hola no es necesario toobe para direcciones enrutables real. Hello siguiente ejemplo también especifica un secreto basado en contraseña, en lugar de generar claves desde dentro de hello portal de Azure. En este momento, la generación de claves no puede realizarse desde Hola CLI de Azure.

Cree una aplicación de Azure Active Directory. Hello en el ejemplo siguiente se crea una aplicación denominada `myAADApp` y utiliza una contraseña de `myPassword`. Especifique su propia contraseña del siguiente modo:

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

Tome nota de hello `applicationId` que se devuelve en la salida de hello de hello anterior comando. Este identificador de la aplicación se utiliza en algunos Hola restantes pasos. A continuación, cree un nombre principal de servicio (SPN) para que la aplicación hello es accesible dentro de su entorno. toosuccessfully cifrar o descifrar los discos virtuales, permisos de clave cifrado de hello almacenados en el almacén de claves deben ser conjunto toopermit hello Azure Active Directory aplicación tooread Hola claves.

Cree Hola SPN y establezca los permisos adecuados de hello como sigue:

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a>Incorporación de un disco virtual y revisión del estado del cifrado
tooactually cifrar algunos discos virtuales, permite agregar un tooan de disco existente de la máquina virtual. Agregue un tooan de disco de datos de 5Gb existente VM como se indica a continuación:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

discos virtuales de Hello no se cifran actualmente. Revisar estado de cifrado actual de hello de la máquina virtual como se indica a continuación:

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a>Cifrado de discos virtuales
toonow cifrar discos virtuales hello, reunir todos los componentes anteriores de hello:

1. Especifique la contraseña y la aplicación de Azure Active Directory hello.
2. Especificar Hola el almacén de claves toostore Hola metadatos para los discos cifrados.
3. Especifique hello toouse de claves criptográficas para hello real cifrado y descifrado.
4. Especifique si desea que tooencrypt disco de SO hello, discos de datos de Hola o todos.

Permite revisar los detalles de Hola para su clave de hello y el almacén de claves de Azure que creó, imprescindible Hola identificador de almacén de claves, URI, y, a continuación, dirección URL de claves en el paso final de hello:

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

Cifrar los discos virtuales con valores obtenidos hello en hello `azure keyvault show` y `azure keyvault key show` comandos como se indica a continuación:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

Como hello comando anterior tiene muchas variables, hello en el ejemplo siguiente se es comando completo de hello como referencia:

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

Hola CLI de Azure no proporciona errores detallados durante el proceso de cifrado de Hola. Para obtener información adicional sobre solución de problemas, revise `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` en hello VM que se va a cifrar.

Por último, permite revisar el estado de cifrado de hello nuevo tooconfirm que los discos virtuales ahora se han cifrado:

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a>Adición de discos de datos adicionales
Una vez que haya cifrado los discos de datos, puede agregar más adelante discos virtuales adicionales tooyour VM y cifrarlas también. Cuando ejecute hello `azure vm enable-disk-encryption` comando, la versión de la secuencia de hello incremento con hello `--sequence-version` parámetro. Este parámetro de versión de secuencia permite tooperform sucesivas operaciones efectuadas sobre Hola misma máquina virtual.

Por ejemplo, permite agregar un segundo tooyour de disco virtual VM como se indica a continuación:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

Vuelva a ejecutar Hola comando tooencrypt Hola discos virtuales, esta vez agrega hello `--sequence-version` parámetro y Hola valor incremental de nuestro primer ejecutar como se indica a continuación:

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


## <a name="next-steps"></a>Pasos siguientes
* Para más información acerca de cómo administrar Azure Key Vault, incluido cómo eliminar claves criptográficas y almacenes, consulte [Administración de Key Vault mediante CLI](../../key-vault/key-vault-manage-with-cli2.md).
* Para obtener más información acerca del cifrado de disco, como preparar una tooAzure tooupload personalizado cifrado de VM, consulte [cifrado del disco de Azure](../../security/azure-security-disk-encryption.md).
