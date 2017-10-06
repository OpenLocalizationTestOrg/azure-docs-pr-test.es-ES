---
title: "aaaUpgrade un almacén de servicios de recuperación tooa de almacén de copia de seguridad (versión preliminar) | Documentos de Microsoft"
description: "Instrucciones y tooupgrade de información de soporte técnico del almacén de la copia de seguridad de Azure tooa del almacén de servicios de recuperación."
services: backup
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
ms.assetid: 228fef19-2f6b-4067-acc3-fb6e501afb88
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/03/2017
ms.author: sogup;markgal;arunak
ms.openlocfilehash: 49062ca4556a009c82f143bb3a60ec71748bed01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-backup-vault-tooa-recovery-services-vault"></a>Actualizar un almacén de servicios de recuperación de tooa de almacén de copia de seguridad

Este artículo explica cómo tooupgrade un almacén de copia de seguridad tooa servicios de recuperación del almacén. proceso de actualización de Hello no afecta a los trabajos de copia de seguridad y se perderá ningún dato de copia de seguridad. Hola principal motivos por los que tooupgrade un tooa de almacén de copia de seguridad del almacén de servicios de recuperación:
- Todas las características de un almacén de Backup se conservan en un almacén de Recovery Services.
- Los almacenes de Recovery Services tienen más características que los de Backup, incluida una mejor seguridad, supervisión integrada, restauraciones más rápidas y restauraciones de nivel de elemento.
- Administran elementos de copia de seguridad desde un portal simplificado y mejorado.
- Características nuevas aplican solo tooRecovery almacenes de servicios.

## <a name="impact-toooperations-during-upgrade"></a>Impacto toooperations durante la actualización

Cuando se actualiza un almacén de servicios de recuperación de tooa de almacén de copia de seguridad, no hay ningún impacto tooyour operaciones de plano de datos. Todos los trabajos de copia de seguridad continúan con normalidad, y los trabajos de restauración activos continúan sin interrupción. Durante la actualización de hello, las operaciones de administración incurre en un corto período de inactividad, y no puede proteger los elementos nuevos o crear trabajos de copias de seguridad de "ad hoc". No se ejecutan trabajos de restauración para las máquinas virtuales IaaS durante la actualización de Hola. actualización de almacén de Hola se realiza en un toocomplete de hora. Una vez finalizado, un almacén de servicios de recuperación reemplaza el almacén de copia de seguridad de Hola.

## <a name="changes-tooyour-automation-and-tool-after-upgrading"></a>Automatización de tooyour de cambios y la herramienta después de actualizar

Al preparar la infraestructura para la actualización del almacén de hello, debe actualizar la automatización existente o herramientas tooensure que TI continúa toowork después de la actualización de Hola.
Consulte las referencias de cmdlets de PowerShell de Hola para hello [modelo de implementación de Service Manager](backup-client-automation-classic.md) hello y [modelo de implementación del Administrador de recursos](backup-client-automation.md).


## <a name="before-you-upgrade"></a>Antes de la actualización

Comprobación de hello problemas siguientes antes de realizar la actualización los almacenes de copia de seguridad tooRecovery almacenes de credenciales de servicio.

- **Versión de agente mínima**: tooupgrade el almacén, asegúrese de agente de servicios de recuperación de Microsoft Azure (MARS) de hello seguro sea al menos la versión 2.0.9070.0. Si el agente de MARS hello es anterior a 2.0.9070.0, actualice el agente de hello antes de iniciar el proceso de actualización de Hola.
- **Modelo de facturación basado en instancias**: almacenes de credenciales de servicio de recuperación sólo admiten el modelo de facturación basado en instancias de Hola. Si tiene un almacén de copia de seguridad que está usando Hola anterior basado en almacenamiento modelo de facturación, convertir el modelo de facturación de Hola durante la actualización.
- **Ninguna operación de configuración de copia de seguridad en curso**: durante la actualización, el plano de administración de toohello de acceso está restringido. Complete todas las acciones de plano de administración y, a continuación, iniciar la actualización de Hola.

## <a name="using-powershell-scripts-tooupgrade-your-vaults"></a>Uso de tooupgrade de secuencias de comandos de PowerShell almacenes

Puede utilizar tooupgrade de secuencias de comandos de PowerShell almacenes de servicios de tooRecovery de almacenes de credenciales de la copia de seguridad. Compruebe que haya Hola requiere actualización de almacén de PowerShell componentes tootrigger Hola. Los scripts de PowerShell para almacenes de Backup no funcionan en los almacenes de Recovery Services. Preparar el entorno de almacenes de Hola tooupgrade:

1. Instalar o actualizar [tooversion Windows Management Framework (WMF) 5](https://www.microsoft.com/download/details.aspx?id=50395) o superior.
2. [Instale el MSI de Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v3.8.0-April2017/azure-powershell.3.8.0.msi).
3. Descargar hello [script de PowerShell](https://aka.ms/vaultupgradescript2) tooupgrade almacenes.

### <a name="run-hello-powershell-script"></a>Ejecutar script de PowerShell de Hola

Usar hello después de la secuencia de comandos tooupgrade almacenes. Hola siguiente secuencia de comandos de ejemplo tiene explicaciones de los parámetros de Hola.

RecoveryServicesVaultUpgrade-1.0.2.ps1 **-SubscriptionID** `<subscriptionID>` **-VaultName** `<vaultname>` **-Location** `<location>` **-ResourceType** `BackupVault` **-TargetResourceGroupName** `<rgname>`

**Id. de suscripción** -Hola número de Id. de suscripción de almacén de Hola que se está actualizando.<br/>
**Nombre de almacén** : hello nombre de almacén de copia de seguridad de Hola que se está actualizando.<br/>
**Ubicación** -ubicación de almacén de Hola que se está actualizando.<br/>
**ResourceType**: Use BackupVault.<br/>
**TargetResourceGroupName** : puesto que va a actualizar Hola almacén tooa basado en el Administrador de recursos de implementación, especifique un grupo de recursos. Puede usar un grupo de recursos existente o crear uno proporcionando un nuevo nombre. Si se escribe incorrectamente el nombre de Hola de un grupo de recursos, puede crear un nuevo grupo de recursos. toolearn más información acerca de los grupos de recursos, lea esta [información general acerca de los grupos de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups).

>[!NOTE]
> Los nombres de grupos de recursos tienen restricciones. Ser seguro toofollow Hola instrucciones; Error toodo por lo que podría provocar toofail de las actualizaciones del almacén.
>
>

Hello fragmento de código siguiente es un ejemplo de qué el comando de PowerShell debería ser similar:

```
RecoveryServicesVaultUpgrade.ps1 -SubscriptionID 53a3c692-5283-4f0a-baf6-49412f5ebefe -VaultName "TestVault" -Location "Australia East" -ResourceType BackupVault -TargetResourceGroupName "ContosoRG"
```

También puede ejecutar script de Hola sin ningún parámetro y se le pregunta tooprovide entradas para todos los parámetros necesarios.

Hola script de PowerShell le pide tooenter sus credenciales. Escriba sus credenciales dos veces: una vez para la cuenta de administrador de servicios de hello y una segunda vez para hello cuenta de administrador de recursos.

### <a name="pre-requisites-checking"></a>Comprobación de los requisitos previos
Una vez que ha escrito sus credenciales de Azure, Azure comprueba que el entorno cumple Hola siguiendo los requisitos previos:

- **Versión de agente mínima** -almacenes de servicios de actualización de copia de seguridad almacenes tooRecovery requiere Hola MARS agente toobe al menos la versión 2.0.9070. Si tiene elementos registrado anteriores a 2.0.9070 tooa el almacén de copia de seguridad con un agente, se produce un error en la comprobación de requisitos previos de Hola. Si se produce un error en la comprobación de requisitos previos de hello, actualice el agente de hello e inténtelo de nuevo almacén de hello tooupgrade. Puede descargar la versión más reciente de Hola de agente de Hola desde [http://download.microsoft.com/download/F/4/B/F4B06356-150F-4DB0-8AD8-95B4DB4BBF7C/MARSAgentInstaller.exe](http://download.microsoft.com/download/F/4/B/F4B06356-150F-4DB0-8AD8-95B4DB4BBF7C/MARSAgentInstaller.exe).
- **Trabajos de configuración en curso**: si alguien está configurando el trabajo para un almacén de copia de seguridad del conjunto de toobe actualizar o registrar un elemento, se produce un error de comprobación de requisitos previos de Hola. Completar configuración de hello, o terminar de registrar el elemento de hello y, a continuación, inicie el proceso de actualización de almacén de Hola.
- **Modelo de facturación de almacenamiento**: servicios de recuperación almacenes compatibilidad Hola basados en instancias modelo de facturación. Si ejecuta la actualización del almacén de hello en un almacén de copia de seguridad que usa Hola modelo de facturación de almacenamiento, puede tooupgrade solicitada del almacén de su modelo de facturación junto con Hola. En caso contrario, se puede actualizar en primer lugar, el modelo de facturación y, a continuación, ejecutar la actualización de almacén de Hola.
- Identificar un grupo de recursos de servicios de recuperación de hello del almacén. Hola a tootake aprovechar características de implementación del Administrador de recursos, debe incluir un almacén de servicios de recuperación en un grupo de recursos. Si no sabe qué toouse de grupo de recursos, proporcionar un proceso de actualización de hello y nombre crea Hola grupo de recursos para usted. proceso de actualización de Hello también asocia el almacén de hello con Hola nuevo grupo de recursos.

Una vez que finalice el proceso de actualización de hello, la comprobación de requisitos previos de hello, proceso de hello le pide toostart Hola almacén actualización. Después de confirmar, proceso de actualización de hello suele tarda alrededor de toocomplete 15-20 minutos, según el tamaño de Hola de su almacén. Si tiene un almacén de gran tamaño, la actualización puede tardar hasta too90 minutos.

## <a name="managing-your-recovery-services-vaults"></a>Administración de almacenes de Recovery Services

Hola después de pantallas muestra un nuevo almacén de servicios de recuperación, actualizado desde el almacén de copia de seguridad, en hello portal de Azure. primera pantalla de Hello muestra el panel de almacén de Hola que muestra las entidades de clave para el almacén de Hola.

![ejemplo de almacén de Recovery Services actualizado desde un almacén de Backup](./media/backup-azure-upgrade-backup-to-recovery-services/upgraded-rs-vault-in-dashboard.png)

pantalla de bienvenida segundo muestra vínculos de Ayuda de hello toohelp disponible empezar a usar servicios de recuperación de hello del almacén.

![vínculos de ayuda en la hoja de inicio rápido de Hola](./media/backup-azure-upgrade-backup-to-recovery-services/quick-start-w-help-links.png)

## <a name="post-upgrade-steps"></a>Pasos posteriores a la actualización
El almacén de Recovery Services admite la especificación de información de zona horaria en la directiva de copia de seguridad. Después de que el almacén se actualiza correctamente, vaya tooBackup directivas desde el menú de configuración de almacén y actualizar la información de zona horaria de Hola para cada una de las directivas de hello configuradas en el almacén de Hola. Esta pantalla ya muestra el tiempo de programación de copia de seguridad de hello especificado como por la zona horaria local utilizada cuando ha creado la directiva. 

## <a name="enhanced-security"></a>Mayor seguridad

Cuando se actualiza un almacén de copia de seguridad del almacén de servicios de recuperación de tooa, configuración de seguridad de Hola para ese almacén se activa automáticamente. Cuando la configuración de seguridad de hello en determinadas operaciones como la eliminación de las copias de seguridad, o para cambiar una frase de contraseña requieren un [la autenticación multifactor Azure](../multi-factor-authentication/multi-factor-authentication.md) PIN. Para obtener más información acerca de la seguridad mejorada de hello, vea el artículo de hello [características de seguridad que las copias de seguridad de tooprotect híbrida](backup-azure-security-feature.md). 

Cuando está activada la seguridad mejorada de hello, los datos se conservan los too14 días después de que se ha eliminado la información de punto de recuperación de hello del almacén de Hola. Se factura a los clientes por el almacenamiento de estos datos de seguridad. Retención de datos de seguridad aplica a puntos de toorecovery de agente de copia de seguridad de Azure de hello, servidor de copia de seguridad de Azure y System Center Data Protection Manager. 

## <a name="gather-data-on-your-vault"></a>Recopilación de datos en el almacén

Una vez que se actualiza el almacén de servicios de recuperación de tooa, configurar los informes de copia de seguridad de Azure (para las máquinas virtuales IaaS y servicios de recuperación de Microsoft Azure (MARS)) y usar informes de Power BI tooaccess Hola. Para obtener más información sobre la recopilación de datos, vea el artículo de hello [Configurar copia de seguridad de Azure notifica](backup-azure-configure-reports.md).

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

**¿Plan de actualización de hello afecta a las copias de seguridad en curso?**</br>
No. Las copias de seguridad en curso continúan sin interrupción durante y después de la actualización.

**Si no tenga previsto actualizar pronto, ¿qué ocurre toomy almacenes?**</br>
Puesto que todas las características nuevas aplican sólo los almacenes de servicios de tooRecovery, le instamos a tooupgrade almacenes. Microsoft finalmente dejará de portal clásico de Hola. A partir del 1 de septiembre de 2017, Microsoft iniciará la actualización automática tooRecovery almacenes de servicios de copia de seguridad de los almacenes de credenciales. Por 1 de noviembre de 2017, Microsoft completará el proceso de actualización de Hola. El almacén se puede actualizar automáticamente en cualquier momento durante septiembre u octubre. Microsoft le recomienda que actualice el almacén tan pronto como sea posible.

**¿Qué supone esta actualización para las herramientas existentes?**</br>
Actualizar el modelo de implementación de administrador de recursos de toohello de herramientas. Servicios de recuperación de almacenes de credenciales se crearon para usan en el modelo de implementación del Administrador de recursos de Hola. Planeación de modelo de implementación del Administrador de recursos de Hola y responden a diferencia de hello en los almacenes son importante. 

**¿Durante la actualización de hello, hay mucho tiempo de inactividad?**</br>
Depende de número de Hola de recursos que se están actualizando. Para implementaciones más pequeñas (de unas decenas de instancias protegidas), actualización completa de hello debe tardar menos de 20 minutos. Para implementaciones grandes, debe tardar una hora como máximo.

**¿Puedo revertir la actualización?**</br>
No. No se admite la reversión después de actualizar correctamente los recursos de Hola.

**¿Se puede validar mi suscripción o recursos toosee si son capaces de actualización?**</br>
Sí. primer paso en la actualización de Hello valida que recursos Hola son capaces de actualización. En caso de error de validación de Hola de requisitos previos, recibir mensajes para todos los motivos de hello no se puede completar la actualización de Hola.

**¿Qué permisos se debe tener tootrigger almacén actualización?**</br>
Hola tooperform del almacén de actualización, se debe agregar como Coadministrador de suscripción de Hola Hola portal de Azure clásico. Esto es necesario incluso si ya aparece como propietario de hello portal de Azure. Intente tooadd Coadministrador de suscripción de hello en Azure toofind portal clásico out si es Coadministrador de suscripción de Hola. Si no es capaz de tooadd un Coadministrador, póngase en contacto con un administrador de servicios o Coadministrador de suscripción de hello, que puede agregar como Coadministrador.

**¿Puedo actualizar mi almacén de Backup basado en CSP?**</br>
No. Actualmente, no se pueden actualizar los almacenes de Backup basados en CSP. Se agregará compatibilidad para actualizar los almacenes de copia de seguridad basada en el CSP en versiones de hello siguientes.

**¿Puedo ver mi almacén clásico después de la actualización?**</br>
No. No se puede ver o administrar su almacén clásico después de la actualización. Solo será capaz de toouse Hola nuevo portal de Azure para todas las acciones de administración en el almacén de Hola.

**Error de la actualización, pero máquina Hola que mantienen el agente de Hola que requieren la actualización, no existe ya. ¿Qué hago en este caso?**</br>
Si necesita almacén de hello toouse, Hola copias de seguridad de este equipo para la retención a largo plazo, no será capaz de tooupgrade el almacén de Hola. En versiones futuras se agregará compatibilidad para actualizar tal almacén.
Si no necesita copias de seguridad de toostore Hola de esta máquina ya, a continuación, por favor, anular el registro de esta máquina desde el almacén de Hola y vuelva a intentar actualización Hola.

**¿Por qué no puedo ver información de los trabajos Hola para los recursos locales después de la actualización**</br>
Supervisión de local de las copias de seguridad (agente de MARS, DPM y el servidor de copia de seguridad de Azure) es una característica nueva que obtendrá al actualizar el almacén de servicios de tooRecovery de almacén de copia de seguridad. información de supervisión de Hello ocupa too12 horas toosync con el servicio de Hola.

**¿Cómo se informa de un problema?**</br>
Si la actualización de cualquier parte del almacén de hello falla, Hola Nota OperationId enumerado en error Hola. Microsoft Support proactivamente funcionará el problema de hello tooresolve. Puede llegar tooSupport o envíenos un correo electrónico en rsvaultupgrade@service.microsoft.com con su Id. de suscripción, el nombre del almacén y OperationId. Problema de hello tooresolve intentaremos realizar tan pronto como sea posible. No vuelva a intentar la operación de Hola a menos que indique explícitamente toodo es así por Microsoft.


## <a name="next-steps"></a>Pasos siguientes
Usar hello artículo al siguiente:</br>
[Copia de seguridad de una máquina virtual de IaaS](backup-azure-arm-vms-prepare.md)</br>
[Copia de seguridad de Azure Backup Server](backup-azure-microsoft-azure-backup.md)</br>
[Hacer una copia de seguridad de Windows Server](backup-configure-vault.md)
