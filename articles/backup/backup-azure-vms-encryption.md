---
title: "aaaBackup y restauración cifrados máquinas virtuales mediante copia de seguridad de Azure"
description: "En este artículo se habla sobre la copia de seguridad de Hola y experiencia de restauración para las máquinas virtuales se cifra mediante el cifrado de disco de Azure."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 8387f186-7d7b-400a-8fc3-88a85403ea63
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/27/2017
ms.author: pajosh;markgal;trinadhk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c19ef6f58e3259949535dab32a55aaf7a8c658fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-encrypted-virtual-machines-with-azure-backup"></a>Cómo tooback seguridad y restauración cifran las máquinas virtuales con copia de seguridad de Azure
En este artículo se habla sobre pasos toobackup y restauración de máquinas virtuales mediante copia de seguridad de Azure. También proporciona detalles acerca de los escenarios admitidos, requisitos previos y pasos para solucionar problemas en los casos de error.

## <a name="supported-scenarios"></a>Escenarios admitidos
> [!NOTE]
> * La copia de seguridad y restauración de máquinas virtuales cifradas solo se admite para máquinas virtuales implementadas con el modelo de Resource Manager. No se admite para máquinas virtuales implementadas con el modelo clásico. <br>
> * Se admite para Windows y Linux máquinas virtuales mediante el cifrado de disco de Azure, que aprovecha la característica BitLocker Hola sector estándar de Windows y la característica de DM Crypt de Linux tooprovide cifrado de discos. <br>
> * Solo se admite para máquinas virtuales cifradas mediante la clave de cifrado de BitLocker y la clave de cifrado de clave. No se admite para máquinas virtuales cifradas solo mediante la clave de cifrado de BitLocker. <br>
>
>

## <a name="prerequisites"></a>Requisitos previos
1. Máquina virtual cifrada mediante [Azure Disk Encryption](../security/azure-security-disk-encryption.md). Se deben cifrar las máquinas virtuales mediante la clave de cifrado de BitLocker y la clave de cifrado de clave (ambas).
2. Se ha creado el almacén de servicios de recuperación y replicación de almacenamiento que se establecen a través de los pasos mencionados en el artículo hello [preparar su entorno para copia de seguridad](backup-azure-arm-vms-prepare.md).
3. Copia de seguridad de Azure se le han otorgado [almacén de claves de permisos tooaccess](#provide-permissions-to-azure-backup) que contiene las claves, cifran de secretos para máquinas virtuales.

## <a name="backup-encrypted-vm"></a>Copia de seguridad cifrada de máquina virtual
Usar Hola siguiente objetivo de copia de seguridad de pasos tooset, definir directivas, configurar elementos y copia de seguridad de desencadenador.

### <a name="configure-backup"></a>Configuración de la copia de seguridad
1. Si ya tiene un almacén de servicios de recuperación abierto, continúe toonext paso. Si no tiene un abierto de almacén de servicios de recuperación, pero están en hello portal de Azure, en el menú del concentrador hello, haga clic en **examinar**.

   * En la lista de Hola de recursos, escriba **servicios de recuperación**.
   * Cuando empiece a escribir, Hola filtros de la lista con los datos especificados. Haga clic en **Almacenes de Recovery Services**cuando lo vea.

      ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     aparece en la lista de Hola de almacenes de servicios de recuperación. En lista de Hola de almacenes de servicios de recuperación, seleccione un almacén.

     de este modo se abrirá el panel de Hello almacén seleccionado.
2. En la lista de Hola de elementos que aparece en el almacén, haga clic en **copia de seguridad** hoja de copia de seguridad de tooopen Hola.

      ![Hoja Backup abierta](./media/backup-azure-vms-encryption/select-backup.png)
3. En la hoja de copia de seguridad de hello, haga clic en **objetivo de copia de seguridad** hoja de tooopen Hola objetivo de copia de seguridad.

      ![Hoja Escenario abierta](./media/backup-azure-vms-encryption/select-backup-goal-one.png)
4. En la hoja de objetivo de copia de seguridad de hello, establezca **donde se está ejecutando la carga de trabajo** tooAzure y **especifique qué desea toobackup** tooVirtual automático, a continuación, haga clic en **Aceptar**.

   hoja de objetivo de copia de seguridad de Hola se cierra y se abre la hoja de directiva de copia de seguridad de Hola.

   ![Hoja Escenario abierta](./media/backup-azure-vms-encryption/select-backup-goal-two.png)
5. En la hoja de la directiva de copia de seguridad de hello, seleccione la directiva de copia de seguridad de Hola que desee tooapply toohello almacén y haga clic en **Aceptar**.

      ![Seleccionar directiva de copia de seguridad](./media/backup-azure-vms-encryption/setting-rs-backup-policy-new.png)

    se muestran detalles de Hello de la directiva predeterminada de hello en los detalles de Hola. Si desea toocreate una directiva, seleccione **crear nuevo** desde el menú desplegable de Hola. Una vez que pulses **Aceptar**, directiva de copia de seguridad de hello está asociado con el almacén de Hola.

    A continuación, elija hello tooassociate de máquinas virtuales con el almacén de Hola.
6. Elija Hola cifra máquinas virtuales tooassociate con hello especifica la directiva y haga clic en **Aceptar**.

      ![Selección de las máquinas virtuales cifradas](./media/backup-azure-vms-encryption/selected-encrypted-vms.png)
7. Esta página muestra un mensaje sobre el almacén de claves seleccionadas asociado toohello cifrado las máquinas virtuales. Servicio de copia de seguridad requiere claves de acceso de solo lectura toohello y secretos en el almacén de claves de Hola. Usa estas claves de toobackup de permisos y secreto, junto con hello asociados a las máquinas virtuales. **Debe conceder permisos toobackup servicio tooaccess el almacén de claves para las copias de seguridad toowork**. Puede proporcionar estos permisos con [pasos enumerados en la siguiente sección de hello](#provide-permissions-to-azure-backup).

      ![Mensaje de máquinas virtuales cifradas](./media/backup-azure-vms-encryption/encrypted-vm-warning-message.png)

      Ahora que ha definido toda la configuración de almacén de hello, en la hoja de copia de seguridad de hello, haga clic en habilitar la copia de seguridad final Hola de página Hola. Habilitar la copia de seguridad implementa el almacén de toohello de directiva de Hola y Hola las máquinas virtuales.
8. Hello siguiente fase de preparación está instalando Agente de máquina virtual de Hola o realizar Hola seguro de agente de máquina virtual está instalado. toodo Hola mismo, siga los pasos de hello mencionados en el artículo hello [preparar su entorno para copia de seguridad](backup-azure-arm-vms-prepare.md).

### <a name="triggering-backup-job"></a>Desencadenamiento del trabajo de copia de seguridad
Siga los pasos de hello mencionados en el artículo hello [almacén de servicios de máquinas virtuales de Azure copia de seguridad toorecovery](backup-azure-arm-vms.md) trabajo de copia de seguridad de tootrigger.

### <a name="continue-backups-of-already-backed-up-vms-with-encryption-enabled"></a>Continuar copias de seguridad de máquinas virtuales ya copiadas con el cifrado habilitado  
Si tiene máquinas virtuales ya que se va a copia de seguridad en el almacén de servicios de recuperación y se han habilitado para el cifrado en un momento posterior, debe dar permisos toobackup servicio tooaccess el almacén de claves para las copias de seguridad toocontinue. Puede proporcionar estos permisos con [los pasos de la siguiente sección de hello](#provide-permissions-to-azure-backup) o mediante PowerShell pasos mencionados en **habilitar la copia de seguridad** sección de [documentación de PowerShell](backup-azure-vms-automation.md). 

## <a name="provide-permissions-tooazure-backup"></a>Proporcionar permisos tooAzure copia de seguridad
Usar hello siguiendo los pasos tooprovide los permisos relevantes tooAzure copia de seguridad tooaccess el almacén de claves y realizar copia de seguridad de máquinas virtuales cifradas:
1. Seleccione **Más servicios** y busque **Key Vaults**.

    ![Búsqueda del almacén de claves](./media/backup-azure-vms-encryption/search-key-vault.png)
    
2. En lista de Hola de almacenes de clave, seleccione el almacén de claves de hello asociado a VM cifrada, que debe toobe copia de seguridad.

     ![Selección de almacén de claves](./media/backup-azure-vms-encryption/select-key-vault.png)
     
3. Haga clic en **Directivas de acceso** y luego en **Agregar nueva**.

    ![Agregar directiva de acceso](./media/backup-azure-vms-encryption/select-key-vault-access-policy.png)
    
4. Haga clic en **principal seleccione** y tipo **servicio de administración de copias de seguridad** en la barra de búsqueda de Hola. 

    ![Búsqueda del servicio de copia de seguridad](./media/backup-azure-vms-encryption/search-backup-service.png)
    
5. Seleccione **Backup Management Service** (Servicio de administración de copias de seguridad) y haga clic en el botón Seleccionar.

    ![Selección del servicio de copia de seguridad](./media/backup-azure-vms-encryption/select-backup-service.png)
    
6. Seleccione **Azure Backup** en el cuadro desplegable Configurar a partir de una plantilla. Rellenan previamente permisos Hola necesario en permisos de clave y secretos permisos de lista desplegable. 

    ![Selección de Azure Backup](./media/backup-azure-vms-encryption/select-backup-template.png)
    
7. Haga clic en **Aceptar**. Tenga en cuenta que Backup Management Service (Servicio de administración de copias de seguridad) se agrega en la hoja Directivas de acceso. 

    ![Directiva de acceso del servicio Backup](./media/backup-azure-vms-encryption/backup-service-access-policy.png)
    
8. Haga clic en **Guardar**. Esto le dará Hola requerido permisos tooAzure copia de seguridad.

    ![Directiva de acceso del servicio Backup](./media/backup-azure-vms-encryption/save-access-policy.png)

Una vez que los permisos se han proporcionado correctamente, puede continuar con la habilitación de la copia de seguridad para VM cifradas.

## <a name="restore-encrypted-vm"></a>Restauración de máquinas virtuales cifradas
toorestore cifrado VM, usar discos de restaurar primero los pasos mencionados en sección **restaurar copia de seguridad discos** en [configuración de restauración de VM elegir](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration). Después de eso, puede usar uno de hello siguientes opciones:
* Usar pasos de PowerShell de hello mencionados en [crear una máquina virtual a partir de discos restaurados](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate completa VM desde discos restaurados.
* OR, [utilizar una plantilla generada como parte de los discos restaurar](backup-azure-arm-restore-vms.md#use-templates-to-customize-restore-vm) toocreate máquinas virtuales desde los discos restaurados. Las plantillas pueden usarse únicamente para los puntos de recuperación creados después del 26 de abril de 2017.

## <a name="troubleshooting-errors"></a>Solución de errores
| Operación | Detalles del error | Resolución |
| --- | --- | --- |
| Backup |La validación produjo un error debido a que la máquina virtual se ha cifrado solo con BEK. Las copias de seguridad se pueden habilitar únicamente para las máquinas virtuales cifradas con BEK y KEK. |Las máquinas virtuales deben cifrarse mediante BEK y KEK. En primer lugar Hola VM de descifrar y cifrar mediante BEK y KEK. Habilite la copia de seguridad una vez que la VM esté cifrada mediante BEK y KEK. Obtener más información acerca de cómo puede [descifrar y cifrar Hola VM](../security/azure-security-disk-encryption.md)  |
| Restauración |No se puede restaurar esta máquina virtual cifrada porque no existe el almacén de claves asociado con esta máquina virtual. |Cree el almacén de claves mediante los pasos descritos en [Introducción a Azure Key Vault](../key-vault/key-vault-get-started.md). Consulte el artículo de hello [restaurar clave de almacén de claves y el secreto mediante copia de seguridad de Azure](backup-azure-restore-key-secret.md) toorestore clave y el secreto si son no está presente. |
| Restauración |No se puede restaurar esta máquina virtual cifrada porque no existe la clave y el secreto asociados con esta máquina virtual. |Consulte el artículo de hello [restaurar clave de almacén de claves y el secreto mediante copia de seguridad de Azure](backup-azure-restore-key-secret.md) toorestore clave y el secreto si son no está presente. |
| Restauración |Servicio de copia de seguridad no tiene recursos tooaccess de autorización en su suscripción. |Como ya se ha indicado, en primer lugar es preciso restaurar los discos, para lo que hay que seguir los pasos especificados en la sección **Restauración de discos de copia de seguridad** de [Elección de una configuración de restauración para una máquina virtual](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration). Después de que éste, usuario PowerShell demasiado[crear una máquina virtual a partir de discos restaurados](backup-azure-vms-automation.md#create-a-vm-from-restored-disks). |
|Backup | Servicio de copia de seguridad de Azure no tiene suficientes permisos tooKey el almacén de copia de seguridad de cifrado las máquinas virtuales | La máquina virtual debe cifrarse con la clave de cifrado BitLocker y la clave de cifrado de claves. Después de eso, debe habilitarse la copia de seguridad.  Servicio de copia de seguridad le proporcionará estos permisos con [pasos enumerados en la sección de hello anterior](#provide-permissions-to-azure-backup) o mediante los pasos de PowerShell mencionados en hello **habilitar la protección** sección de hello PowerShell documentación en [tooback de cmdlets de uso AzureRM.RecoveryServices.Backup las máquinas virtuales](backup-azure-vms-automation.md#back-up-azure-vms). |  
