---
ms.assetid: 
title: "aaaAzure del almacén de claves: cómo eliminar toouse automático con CLI"
description: "Ejemplos de casos de uso de eliminación temporal con fragmentos de código de la CLI"
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 672f5210ab119c244ca712f0bb80b653b50ea79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-key-vault-soft-delete-with-cli"></a>Cómo toouse el almacén de claves soft-delete con CLI

La característica de eliminación temporal de Azure Key Vault permite recuperar almacenes y objetos de almacenes eliminados. En concreto, soft-delete Hola direcciones los escenarios siguientes:

- Compatibilidad con la eliminación recuperable de una instancia de Key Vault
- Compatibilidad con la eliminación recuperable de objetos de Key Vault: claves, secretos y certificados

## <a name="prerequisites"></a>Requisitos previos

- CLI de Azure 2.0: si no tiene esta configuración para su entorno, consulte [Administración de Key Vault mediante CLI 2.0](key-vault-manage-with-cli2.md).

Para obtener información de referencia específica sobre Key Vault para la CLI, consulte la [referencia de Key Vault para la CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/keyvault).

## <a name="required-permissions"></a>Permisos necesarios

Las operaciones de Key Vault se administran por separado mediante los permisos de control de acceso basado en roles (RBAC) como se indica a continuación:

| Operación | Descripción | Permiso del usuario |
|:--|:--|:--|
|Enumerar|Enumera los almacenes de claves eliminados.|Microsoft.KeyVault/deletedVaults/read|
|Recuperar|Restaura un almacén de claves eliminado.|Microsoft.KeyVault/vaults/write|
|Purgar|Elimina permanentemente un almacén de claves eliminado y todo su contenido.|Microsoft.KeyVault/locations/deletedVaults/purge/action|

Para más información sobre los permisos y el control de acceso, consulte [Protección de un almacén de claves](key-vault-secure-your-key-vault.md).

## <a name="enabling-soft-delete"></a>Habilitar la eliminación temporal

toobe puede toorecover del almacén de objetos almacenados en una clave o un almacén de claves se eliminó, primero debe habilitar la eliminación de software para ese almacén de claves.

### <a name="existing-key-vault"></a>Almacén de claves existente

Para un almacén de claves existente denominado ContosoVault, habilite la eliminación temporal como se indica a continuación. 

>[!NOTE]
>Actualmente necesita Hola de escritura de toouse Azure Resource Manager recursos manipulación toodirectly *enableSoftDelete* toohello recursos de almacén de claves de propiedad.

```azurecli
az resource update --id $(az keyvault show --name ContosoVault -o tsv | awk '{print $1}') --set properties.enableSoftDelete=true
```

### <a name="new-key-vault"></a>Almacén de claves nuevo

Habilitar la eliminación de software para un nuevo almacén de claves se realiza en el momento de creación mediante la adición de marca de soft-delete enable hello tooyour crear comando.

```azurecli
az keyvault create --name ContosoVault --resource-group ContosoRG --enable-soft-delete true --location westus
```

### <a name="verify-soft-delete-enablement"></a>Comprobación de la habilitación de la eliminación temporal

tooverify que un almacén de claves tiene habilitado, soft-delete Hola ejecución *mostrar* de comandos y busque hello 'Suave eliminar Enabled?' y su valor, true o false.

```azurecli
az keyvault show --name ContosoVault
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a>Eliminación de un almacén de claves protegido por eliminación temporal

Hola comando toodelete (o quitar) un almacén de claves permanece Hola mismo, pero sus cambios de comportamiento dependen de si ha habilitado soft-delete o no.

```azurecli
az keyvault delete --name ContosoVault
```

> [!IMPORTANT]
>Si ejecuta el comando anterior de Hola para un almacén de claves que no tiene habilitada la eliminación temporal, se eliminará permanentemente este almacén de claves y todo su contenido sin ninguna opción para la recuperación.

### <a name="how-soft-delete-protects-your-key-vaults"></a>Uso de la eliminación temporal para proteger los almacenes de claves

Con la eliminación temporal habilitada:

- Cuando se elimina un almacén de claves, se quita de su grupo de recursos y se coloca en un espacio de nombres reservado que solo está asociado a la ubicación de Hola donde se creó. 
- Objetos de una clave eliminada del almacén, como las claves, secretos y certificados, son inaccesibles y mantenerse así mientras su almacén de claves que lo contiene está en estado de hello eliminado. 
- nombre DNS de Hola para un almacén de claves en un estado de eliminación se sigue reservando por lo tanto, no se puede crear un nuevo almacén de claves con el mismo nombre.  

Puede ver almacenes de clave de estado eliminado, asociados a su suscripción, con hello siguiente comando:

```azurecli
az keyvault list-deleted
```

Hola *Id. de recurso* Hola salida hace referencia toohello de identificador de recurso original de este almacén. Puesto que este almacén de claves está ahora en estado eliminado, no existe ningún recurso con ese identificador de recurso. Hola *identificador* campo puede ser recurso de Hola de tooidentify usado durante la recuperación o purgar. Hola *programada fecha purgar* campo indica al almacén de Hola se eliminarán permanentemente (purga) si no se realiza ninguna acción para este almacén eliminado. Hola toocalculate período, que se usa de Hello predeterminado retención *programada fecha purgar*, es de 90 días.

## <a name="recovering-a-key-vault"></a>Recuperación de un almacén de claves

toorecover un almacén de claves, necesita nombre de almacén de claves de hello toospecify, grupo de recursos y ubicación. Nota Hola hello y ubicación del grupo de recursos del programa Hola a elimina el almacén de claves según sea necesario para un proceso de recuperación del almacén de claves.

```azurecli
az keyvault recover --location westus --name ContosoVault
```

Cuando se recupera un almacén de claves, el resultado de hello es un nuevo recurso con el identificador de recurso original. del almacén de hello claves Si se ha quitado el grupo de recursos de Hola donde existía el almacén de claves de hello, debe crearse un nuevo grupo de recursos con el mismo nombre antes de que se puede recuperar el almacén de claves de Hola.

## <a name="key-vault-objects-and-soft-delete"></a>Objetos de Key Vault y eliminación temporal

Si tiene una clave, "ContosoFirstKey", en un almacén de claves denominado "ContosoVault" con eliminación temporal habilitada, este es el procedimiento para eliminarla.

```azurecli
az keyvault key delete --name ContosoFirstKey --vault-name ContosoVault
```

Con el almacén de claves habilitado para la eliminación temporal, una clave eliminada seguirá apareciendo como eliminada excepto si enumera o recupera explícitamente las claves eliminadas. Se producirá un error de mayoría de las operaciones en una clave de estado de hello eliminado excepto para enumerar una clave eliminada, recuperarlo o purgar. 

Por ejemplo, las claves de toolist eliminar toorequest en un almacén de claves, utilizar Hola siguiente comando:

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="transition-state"></a>Estado de transición 

Cuando se elimina una clave en un almacén de claves con la eliminación de software habilitada, puede tardar unos segundos hello toocomplete de transición. Durante este estado de transición, puede aparecer que esa clave hello no está en estado activo de Hola u Hola eliminado. Este comando permite enumerar todas las claves eliminadas en el almacén de claves denominado "ContosoVault".

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="using-soft-delete-with-key-vault-objects"></a>Uso de la eliminación temporal con objetos de almacén de claves

Igual que los almacenes de claves, una clave eliminada, secreto o certificado permanecerá en estado de eliminación para los días de too90 a menos que recuperarlo o lo purga. 

#### <a name="keys"></a>simétricas

toorecover una clave eliminada:

```azurecli
az keyvault key recover --name ContosoFirstKey --vault-name ContosoVault
```

toopermanently eliminar una clave:

```azurecli
az keyvault key purge --name ContosoFirstKey --vault-name ContosoVault
```

>[!NOTE]
>Si purga una clave se eliminará permanentemente, lo que significa que no se podrá recuperar de nuevo.

Hola **recuperar** y **purgar** las acciones tienen sus propios permisos asociados en una directiva de acceso del almacén de claves. Para una tooexecute de capaz de toobe principal de usuario o servicio un **recuperar** o **purgar** acción que deben tener permiso respectivos Hola para ese objeto (clave o el secreto) en directiva de acceso del almacén de claves de Hola. De forma predeterminada, Hola **purgar** permiso no se agrega la directiva de acceso del almacén de tooa claves cuando contextual 'all' hello es toogrant usado todos los datos de usuario de tooa de permisos. Debe conceder el permiso de **purga** de forma explícita. Por ejemplo, Hola después concede comando user@contoso.com tooperform permiso varias operaciones de claves de *ContosoVault* incluidos **purgar**.

#### <a name="set-a-key-vault-access-policy"></a>Establecimiento de una directiva de acceso del almacén de claves

```azurecli
az keyvault set-policy --name ContosoVault --key-permissions get create delete list update import backup restore recover purge
```

>[!NOTE] 
> Si tiene un almacén de claves existente para el que se acaba de habilitar la eliminación temporal, puede que no tenga los permisos de **recuperación** y **purga**.

#### <a name="secrets"></a>Secretos

Al igual que con las claves, se trabaja con los secretos de un almacén de claves con sus propios comandos. Después, son comandos de Hola para eliminar, enumerar, recuperación y purga de secretos.

- Elimine un secreto llamado SQLPassword: 
```azurecli
az keyvault secret delete --vault-name ContosoVault -name SQLPassword
```

- Enumere todos los secretos eliminados de un almacén de claves: 
```azurecli
az keyvault secret list-deleted --vault-name ContosoVault
```

- Recuperar un secreto en estado de hello eliminado: 
```azurecli
az keyvault secret recover --name SQLPassword --vault-name ContosoVault
```

- Purgue un secreto en el estado eliminado: 
```azurecli
az keyvault secret purge --name SQLPAssword --vault-name ContosoVault
```

>[!NOTE]
>Si purga un secreto se eliminará permanentemente, lo que significa que no se podrá recuperar de nuevo.

## <a name="purging-and-key-vaults"></a>Purga y almacenes de claves

### <a name="key-vault-objects"></a>Objetos de almacén de claves

Si purga una clave, un secreto o un certificado se eliminarán permanentemente, lo que significa que no se podrán recuperar de nuevo. almacén de claves de Hola que contenía Hola Eliminar objeto sin embargo permanecerán intacto así como todos los demás objetos de almacén de claves de Hola. 

### <a name="key-vaults-as-containers"></a>Almacenes de claves como contenedores
Cuando se purga un almacén de claves, todo su contenido, incluidas las claves, los secretos y los certificados, se eliminan permanentemente. toopurge un almacén de claves, use hello `az keyvault purge` comando. Puede encontrar ubicación Hola almacenes de clave eliminada la suscripción con el comando de hello `az keyvault list-deleted`.

```azurecli
az keyvault purge --location westus --name ContosoVault
```

>[!NOTE]
>Si purga un almacén de claves se eliminará permanentemente, lo que significa que no se podrá recuperar de nuevo.

### <a name="purge-permissions-required"></a>Se requieren permisos de purga
- toopurge un almacén de claves eliminado, tal que el almacén de Hola y todo su contenido se quita de forma permanente, Hola usuario necesita RBAC permiso tooperform una *Microsoft.KeyVault/locations/deletedVaults/purge/action* operación. 
- clave de hello eliminado de toolist, almacén Hola un usuario tiene RBAC permiso tooperform *Microsoft.KeyVault/deletedVaults/read* permiso. 
- Solo un administrador de suscripción tiene estos permisos. 

### <a name="scheduled-purge"></a>Purga programada

Enumerar los objetos de almacén de claves eliminadas muestra cuándo son toobe schedled purgado por el almacén de claves. Hola *programada fecha purgar* campo indica cuando un objeto de almacén de claves se eliminará permanentemente, si se realiza ninguna acción. De forma predeterminada, el período de retención de Hola para un objeto de almacén de claves eliminadas es 90 días.

>[!NOTE]
>Un objeto de almacén purgado, desencadenado por el valor de su campo de *fecha de purga programada*, se eliminará permanentemente. No se podrá volver a recuperar.

## <a name="other-resources"></a>Otros recursos:

- Para obtener una información general sobre la nueva característica de eliminación temporal, consulte [la información general sobre la eliminación temporal de Azure Key Vault](key-vault-ovw-soft-delete.md).
- Para obtener una descripción general del uso de Azure Key Vault, consulte [Introducción a Azure Key Vault](key-vault-get-started.md).

