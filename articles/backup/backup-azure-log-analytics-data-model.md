---
title: "modelo de datos de análisis de aaaLog de copia de seguridad de Azure"
description: "En este artículo se explican los detalles del modelo de datos de Log Analytics para los datos de Azure Backup."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: dfd5c73d-0d34-4d48-959e-1936986f9fc0
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 04ac16e38b896851f60b1c4ffbea4343347ae32c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-data-model-for-azure-backup-data"></a>Modelo de datos de Log Analytics para datos de Azure Backup
Este artículo describe el modelo de datos de hello utilizado para insertar informes datos tooLog análisis. Con este modelo de datos, puede crear consultas personalizadas y paneles y utilizarlos en OMS. 

## <a name="using-azure-backup-data-model"></a>Uso del modelo de datos de Azure Backup
Puede usar Hola siguiendo los campos que se proporcionan como parte de los objetos visuales toocreate de modelo de datos de Hola y consultas personalizadas, panel según sus requisitos.

### <a name="alert"></a>Alerta
Esta tabla proporciona detalles acerca de los campos relacionados con la alerta.

| Campo | Tipo de datos | Descripción |
| --- | --- | --- |
| AlertUniqueId_s |Texto |Identificador único de hello generó la alerta |
| AlertType_s |Texto |Tipo de hello generó la alerta, por ejemplo, copia de seguridad |
| AlertStatus_s |Texto |Estado de alerta hello, por ejemplo, activo |
| AlertOccurenceDateTime_s |Fecha y hora |Fecha y hora en que se creó la alerta |
| AlertSeverity_s |Texto |Gravedad de alerta hello, por ejemplo, crítico |
| EventName_s |Texto |Este campo representa el nombre de este evento; es siempre AzureBackupCentralReport |
| BackupItemUniqueId_s |Texto |Identificador único de toowhich de copia de seguridad de elemento de hello que esta alerta pertenece demasiado|
| SchemaVersion_s |Texto |Este campo indica la versión actual del esquema de hello, resulta **V1** |
| State_s |Texto |Estado actual del objeto de alerta de hello, por ejemplo, activo, eliminado |
| BackupManagementType_s |Texto |Tipo de proveedor para realizar la copia de seguridad, por ejemplo, IaaSVM, toowhich FileFolder esta alerta pertenece demasiado|
| nombreOperación |Texto |Este campo representa el nombre de la operación actual de hello - alerta |
| Categoría |Texto |Este campo representa la categoría de datos de diagnóstico que se insertan tooLog análisis, entonces se AzureBackupReport |
| Recurso |Texto |Se trata de recursos de hello para el que se está recopilando datos, muestra el nombre del almacén de servicios de recuperación |
| ProtectedServerUniqueId_s |Texto |Identificador único de hello protegido toowhich que esta alerta pertenece demasiado|
| VaultUniqueId_s |Texto |Identificador único de hello protegido toowhich que esta alerta pertenece demasiado|
| SourceSystem |Texto |Sistema de origen de datos actual de hello - Azure |
| ResourceId |Texto |Este campo representa el id. de recurso para el que se están recopilando datos; muestra el id. de recurso del almacén de Recovery Services |
| SubscriptionId |Texto |Este campo representa el identificador de la suscripción de recursos hello (almacén RS) para el que se está recopilando datos |
| ResourceGroup |Texto |Este campo representa el grupo de recursos del recurso de hello (almacén RS) para el que se está recopilando datos |
| ResourceProvider |Texto |Este campo representa el proveedor de recursos de hello para el que se están recopilando datos - Microsoft.RecoveryServices |
| ResourceType |Texto |Este campo representa el tipo de recurso de hello para el que se están recopilando datos - almacenes |

### <a name="backupitem"></a>BackupItem
Esta tabla proporciona detalles acerca de los campos relacionados con el elemento de copia de seguridad.

| Campo | Tipo de datos | Descripción |
| --- | --- | --- |
| EventName_s |Texto |Este campo representa el nombre de este evento; es siempre AzureBackupCentralReport |  
| BackupItemUniqueId_s |Texto |Identificador único del elemento de copia de seguridad de Hola |
| BackupItemId_s |Texto |Identificador de elemento de copia de seguridad |
| BackupItemName_s |Texto |Nombre de elemento de copia de seguridad |
| BackupItemFriendlyName_s |Texto |Nombre descriptivo del elemento de copia de seguridad |
| BackupItemType_s |Texto |Tipo de elemento de copia de seguridad, por ejemplo, VM o FileFolder |
| ProtectedServerName_s |Texto |Nombre de elemento de copia de seguridad de servidor protegido toowhich pertenece demasiado|
| ProtectionState_s |Texto |Estado de protección actual del elemento de copia de seguridad de hello, por ejemplo, Protected, ProtectionStopped |
| SchemaVersion_s |Texto |Este campo indica la versión actual del esquema de hello, resulta **V1** |
| State_s |Texto |Estado actual del objeto de elemento de copia de seguridad de hello, por ejemplo, activo, eliminado |
| BackupManagementType_s |Texto |Tipo de proveedor para realizar la copia de seguridad, por ejemplo, IaaSVM, toowhich FileFolder pertenece este elemento de copia de seguridad demasiado|
| nombreOperación |Texto |Este campo representa el nombre de la operación actual de hello - copia de seguridad |
| Categoría |Texto |Este campo representa la categoría de datos de diagnóstico que se insertan tooLog análisis, entonces se AzureBackupReport |
| Recurso |Texto |Se trata de recursos de hello para el que se está recopilando datos, muestra el nombre del almacén de servicios de recuperación |
| SourceSystem |Texto |Sistema de origen de datos actual de hello - Azure |
| ResourceId |Texto |Este campo representa el id. de recurso para el que se están recopilando datos; muestra el id. de recurso del almacén de Recovery Services |
| SubscriptionId |Texto |Este campo representa el identificador de la suscripción de recursos hello (almacén RS) para el que se está recopilando datos |
| ResourceGroup |Texto |Este campo representa el grupo de recursos del recurso de hello (almacén RS) para el que se está recopilando datos |
| ResourceProvider |Texto |Este campo representa el proveedor de recursos de hello para el que se están recopilando datos - Microsoft.RecoveryServices |
| ResourceType |Texto |Este campo representa el tipo de recurso de hello para el que se están recopilando datos - almacenes |

### <a name="backupitemassociation"></a>BackupItemAssociation
Esta tabla proporciona detalles acerca de las asociaciones de elementos de copia de seguridad con varias entidades.

| Campo | Tipo de datos | Descripción |
| --- | --- | --- |
| EventName_s |Texto |Este campo representa el nombre de este evento; es siempre AzureBackupCentralReport |  
| BackupItemUniqueId_s |Texto |Identificador único del elemento de copia de seguridad de Hola |
| SchemaVersion_s |Texto |Este campo indica la versión actual del esquema de hello, resulta **V1** |
| State_s |Texto |Estado actual del objeto de asociación de copia de seguridad de elemento hello, por ejemplo, activo, eliminado |
| BackupManagementType_s |Texto |Tipo de proveedor para realizar la copia de seguridad, por ejemplo, IaaSVM, toowhich FileFolder pertenece este elemento de copia de seguridad demasiado|
| nombreOperación |Texto |Este campo representa el nombre de la operación actual de hello - BackupItemAssociation |
| Categoría |Texto |Este campo representa la categoría de datos de diagnóstico que se insertan tooLog análisis, entonces se AzureBackupReport |
| Recurso |Texto |Se trata de recursos de hello para el que se está recopilando datos, muestra el nombre del almacén de servicios de recuperación |
| PolicyUniqueId_g |Texto |Id. tooidentify Hola directiva único, el elemento de copia de seguridad que está asociado demasiado|
| ProtectedServerUniqueId_s |Texto |Identificador único de hello protegido toowhich de servidor que pertenece este elemento de copia de seguridad demasiado|
| VaultUniqueId_s |Texto |Identificador único de hello almacén toowhich que pertenece este elemento de copia de seguridad demasiado|
| SourceSystem |Texto |Sistema de origen de datos actual de hello - Azure |
| ResourceId |Texto |Este campo representa el id. de recurso para el que se están recopilando datos; muestra el id. de recurso del almacén de Recovery Services |
| SubscriptionId |Texto |Este campo representa el identificador de la suscripción de recursos hello (almacén RS) para el que se está recopilando datos |
| ResourceGroup |Texto |Este campo representa el grupo de recursos del recurso de hello (almacén RS) para el que se está recopilando datos |
| ResourceProvider |Texto |Este campo representa el proveedor de recursos de hello para el que se están recopilando datos - Microsoft.RecoveryServices |
| ResourceType |Texto |Este campo representa el tipo de recurso de hello para el que se están recopilando datos - almacenes |

### <a name="job"></a>Trabajo
Esta tabla proporciona detalles acerca de los campos relacionados con los trabajos.

| Campo | Tipo de datos | Descripción |
| --- | --- | --- |
| EventName_s |Texto |Este campo representa el nombre de este evento; es siempre AzureBackupCentralReport |
| BackupItemUniqueId_s |Texto |Identificador único de toowhich de copia de seguridad de elemento de hello que pertenece demasiado este trabajo|
| SchemaVersion_s |Texto |Este campo indica la versión actual del esquema de hello, resulta **V1** |
| State_s |Texto |Estado actual del objeto de trabajo de hello, por ejemplo, activo, eliminado |
| BackupManagementType_s |Texto |Tipo de proveedor para realizar la copia de seguridad, por ejemplo, IaaSVM, toowhich FileFolder pertenece demasiado este trabajo|
| nombreOperación |Texto |Este campo representa el nombre de la operación actual de hello - trabajo |
| Categoría |Texto |Este campo representa la categoría de datos de diagnóstico que se insertan tooLog análisis, entonces se AzureBackupReport |
| Recurso |Texto |Se trata de recursos de hello para el que se está recopilando datos, muestra el nombre del almacén de servicios de recuperación |
| ProtectedServerUniqueId_s |Texto |Identificador único de hello protegido toowhich que pertenece demasiado este trabajo|
| VaultUniqueId_s |Texto |Identificador único de hello protegido toowhich que pertenece demasiado este trabajo|
| JobOperation_s |Texto |Operación para la que se ejecuta el trabajo, por ejemplo, Backup, Restore o Configure Backup |
| JobStatus_s |Texto |Estado de hello finalizó el trabajo, por ejemplo, completado, error |
| JobFailureCode_s |Texto |Cadena del código de error por el que produjo el error del trabajo |
| JobStartDateTime_s |Fecha y hora |Fecha y hora en las que comenzó la ejecución del trabajo |
| BackupStorageDestination_s |Texto |Destino de almacenamiento de almacenamiento de copias de seguridad, por ejemplo, Cloud o Disk  |
| JobDurationInSecs_s | Number |Duración del trabajo total en segundos |
| DataTransferredInMB_s | Number |Datos transferidos en MB para este trabajo|
| JobUniqueId_g |Texto |Trabajo de hello tooidentify de Id. único |
| SourceSystem |Texto |Sistema de origen de datos actual de hello - Azure |
| ResourceId |Texto |Este campo representa el id. de recurso para el que se están recopilando datos; muestra el id. de recurso del almacén de Recovery Services |
| SubscriptionId |Texto |Este campo representa el identificador de la suscripción de recursos hello (almacén RS) para el que se está recopilando datos |
| ResourceGroup |Texto |Este campo representa el grupo de recursos del recurso de hello (almacén RS) para el que se está recopilando datos |
| ResourceProvider |Texto |Este campo representa el proveedor de recursos de hello para el que se están recopilando datos - Microsoft.RecoveryServices |
| ResourceType |Texto |Este campo representa el tipo de recurso de hello para el que se están recopilando datos - almacenes |

### <a name="policy"></a>Directiva
Esta tabla proporciona detalles acerca de los campos relacionados con las directivas.

| Campo | Tipo de datos | Descripción |
| --- | --- | --- |
| EventName_s |Texto |Este campo representa el nombre de este evento; es siempre AzureBackupCentralReport |
| SchemaVersion_s |Texto |Este campo indica la versión actual del esquema de hello, resulta **V1** |
| State_s |Texto |Estado actual del objeto de directiva de hello, por ejemplo, activo, eliminado |
| BackupManagementType_s |Texto |Tipo de proveedor para realizar la copia de seguridad, por ejemplo, IaaSVM, toowhich FileFolder esta directiva pertenece demasiado|
| nombreOperación |Texto |Este campo representa el nombre de la operación actual de hello - directiva |
| Categoría |Texto |Este campo representa la categoría de datos de diagnóstico que se insertan tooLog análisis, entonces se AzureBackupReport |
| Recurso |Texto |Se trata de recursos de hello para el que se está recopilando datos, muestra el nombre del almacén de servicios de recuperación |
| PolicyUniqueId_g |Texto |Directiva de hello tooidentify de Id. único |
| PolicyName_s |Texto |Nombre de directiva de hello definida |
| BackupFrequency_s |Texto |Frecuencia con la que se ejecutan las copias de seguridad, por ejemplo, a diario o semanalmente |
| BackupTimes_s |Texto |Fecha y hora en que se programan las copias de seguridad |
| BackupDaysOfTheWeek_s |Texto |Días de la semana de hello cuando se hayan programado las copias de seguridad |
| RetentionDuration_s |Número entero |Duración de retención de las copias de seguridad configuradas |
| DailyRetentionDuration_s |Número entero |Duración de retención total de las copias de seguridad configuradas, en días |
| DailyRetentionTimes_s |Texto |Fecha y hora en que se configuró la retención diaria |
| WeeklyRetentionDuration_s |Número decimal |Duración total de la retención semanal de las copias de seguridad configuradas, en semanas |
| WeeklyRetentionTimes_s |Texto |Fecha y hora en que se ha configurado la retención semanal |
| WeeklyRetentionDaysOfTheWeek_s |Texto |Días de la semana de hello seleccionado para la retención semanal |
| MonthlyRetentionDuration_s |Número decimal |Duración de retención total de las copias de seguridad configuradas, en meses |
| MonthlyRetentionTimes_s |Texto |Fecha y hora en que se ha configurado la retención mensual |
| MonthlyRetentionFormat_s |Texto |Tipo de configuración para la retención mensual ,por ejemplo, diariamente si se basa en día, semanalmente si se basa en semana |
| MonthlyRetentionDaysOfTheWeek_s |Texto |Días de la semana de hello seleccionado para la retención mensual |
| MonthlyRetentionWeeksOfTheMonth_s |Texto |Semanas del mes de hello cuando se configura la retención mensual, por ejemplo, primero, último etcetera. |
| YearlyRetentionDuration_s |Número decimal |Duración total de la retención de las copias de seguridad configuradas, en años |
| YearlyRetentionTimes_s |Texto |Fecha y hora en que se ha configurado la retención anual |
| YearlyRetentionMonthsOfTheYear_s |Texto |Meses del año de hello seleccionado para retención anual |
| YearlyRetentionFormat_s |Texto |Tipo de configuración para la retención anual ,por ejemplo, diariamente si se basa en día, semanalmente si se basa en semana |
| YearlyRetentionDaysOfTheMonth_s |Texto |Fechas del mes de hello seleccionado para retención anual |
| SourceSystem |Texto |Sistema de origen de datos actual de hello - Azure |
| ResourceId |Texto |Este campo representa el id. de recurso para el que se están recopilando datos; muestra el id. de recurso del almacén de Recovery Services |
| SubscriptionId |Texto |Este campo representa el identificador de la suscripción de recursos hello (almacén RS) para el que se está recopilando datos |
| ResourceGroup |Texto |Este campo representa el grupo de recursos del recurso de hello (almacén RS) para el que se está recopilando datos |
| ResourceProvider |Texto |Este campo representa el proveedor de recursos de hello para el que se están recopilando datos - Microsoft.RecoveryServices |
| ResourceType |Texto |Este campo representa el tipo de recurso de hello para el que se están recopilando datos - almacenes |

### <a name="policyassociation"></a>PolicyAssociation
Esta tabla proporciona detalles acerca de las asociaciones de directivas con varias entidades.

| Campo | Tipo de datos | Descripción |
| --- | --- | --- |
| EventName_s |Texto |Este campo representa el nombre de este evento; es siempre AzureBackupCentralReport |
| SchemaVersion_s |Texto |Este campo indica la versión actual del esquema de hello, resulta **V1** |
| State_s |Texto |Estado actual del objeto de directiva de hello, por ejemplo, activo, eliminado |
| BackupManagementType_s |Texto |Tipo de proveedor para realizar la copia de seguridad, por ejemplo, IaaSVM, toowhich FileFolder esta directiva pertenece demasiado|
| nombreOperación |Texto |Este campo representa el nombre de la operación actual de hello - PolicyAssociation |
| Categoría |Texto |Este campo representa la categoría de datos de diagnóstico que se insertan tooLog análisis, entonces se AzureBackupReport |
| Recurso |Texto |Se trata de recursos de hello para el que se está recopilando datos, muestra el nombre del almacén de servicios de recuperación |
| PolicyUniqueId_g |Texto |Directiva de hello tooidentify de Id. único |
| VaultUniqueId_s |Texto |Identificador único de hello almacén toowhich que esta directiva pertenece demasiado|
| SourceSystem |Texto |Sistema de origen de datos actual de hello - Azure |
| ResourceId |Texto |Este campo representa el id. de recurso para el que se están recopilando datos; muestra el id. de recurso del almacén de Recovery Services |
| SubscriptionId |Texto |Este campo representa el identificador de la suscripción de recursos hello (almacén RS) para el que se está recopilando datos |
| ResourceGroup |Texto |Este campo representa el grupo de recursos del recurso de hello (almacén RS) para el que se está recopilando datos |
| ResourceProvider |Texto |Este campo representa el proveedor de recursos de hello para el que se están recopilando datos - Microsoft.RecoveryServices |
| ResourceType |Texto |Este campo representa el tipo de recurso de hello para el que se están recopilando datos - almacenes |

### <a name="protectedserver"></a>ProtectedServer
Esta tabla proporciona detalles acerca de los campos relacionados con el servidor protegido.

| Campo | Tipo de datos | Descripción |
| --- | --- | --- |
| EventName_s |Texto |Este campo representa el nombre de este evento; es siempre AzureBackupCentralReport |
| ProtectedServerName_s |Texto |Nombre del servidor protegido |
| SchemaVersion_s |Texto |Este campo indica la versión actual del esquema de hello, resulta **V1** |
| State_s |Texto |Estado actual de hello protegido objeto de servidor, por ejemplo, activo, eliminado |
| BackupManagementType_s |Texto |Tipo de proveedor para realizar la copia de seguridad, por ejemplo, IaaSVM, toowhich FileFolder pertenece demasiado este servidor protegido|
| nombreOperación |Texto |Este campo representa el nombre de la operación actual de hello - ProtectedServer |
| Categoría |Texto |Este campo representa la categoría de datos de diagnóstico que se insertan tooLog análisis, entonces se AzureBackupReport |
| Recurso |Texto |Se trata de recursos de hello para el que se está recopilando datos, muestra el nombre del almacén de servicios de recuperación |
| ProtectedServerUniqueId_s |Texto |Identificador único de hello servidor protegido |
| RegisteredContainerId_s |Texto |Identificador de contenedor registrado para copia de seguridad |
| ProtectedServerType_s |Texto |Tipo de servidor protegido del que se realiza la copia de seguridad, por ejemplo, Windows |
| ProtectedServerFriendlyName_s |Texto |Nombre descriptivo del servidor protegido |
| AzureBackupAgentVersion_s |Texto |Número de versión de Azure Backup Agent |
| SourceSystem |Texto |Sistema de origen de datos actual de hello - Azure |
| ResourceId |Texto |Este campo representa el id. de recurso para el que se están recopilando datos; muestra el id. de recurso del almacén de Recovery Services |
| SubscriptionId |Texto |Este campo representa el identificador de la suscripción de recursos hello (almacén RS) para el que se está recopilando datos |
| ResourceGroup |Texto |Este campo representa el grupo de recursos del recurso de hello (almacén RS) para el que se está recopilando datos |
| ResourceProvider |Texto |Este campo representa el proveedor de recursos de hello para el que se están recopilando datos - Microsoft.RecoveryServices |
| ResourceType |Texto |Este campo representa el tipo de recurso de hello para el que se están recopilando datos - almacenes |

### <a name="protectedserverassociation"></a>ProtectedServerAssociation
Esta tabla proporciona detalles acerca de las asociaciones de servidores protegidos con otras entidades.

| Campo | Tipo de datos | Descripción |
| --- | --- | --- |
| EventName_s |Texto |Este campo representa el nombre de este evento; es siempre AzureBackupCentralReport |
| SchemaVersion_s |Texto |Este campo indica la versión actual del esquema de hello, resulta **V1** |
| State_s |Texto |Estado actual de hello protegido objeto de asociación de servidor, por ejemplo, activo, eliminado |
| BackupManagementType_s |Texto |Tipo de proveedor para realizar la copia de seguridad, por ejemplo, IaaSVM, toowhich FileFolder pertenece demasiado este servidor protegido|
| nombreOperación |Texto |Este campo representa el nombre de la operación actual de hello - ProtectedServerAssociation |
| Categoría |Texto |Este campo representa la categoría de datos de diagnóstico que se insertan tooLog análisis, entonces se AzureBackupReport |
| Recurso |Texto |Se trata de recursos de hello para el que se está recopilando datos, muestra el nombre del almacén de servicios de recuperación |
| ProtectedServerUniqueId_s |Texto |Identificador único de hello servidor protegido |
| VaultUniqueId_s |Texto |Identificador único de hello almacén toowhich que pertenece demasiado este servidor protegido|
| SourceSystem |Texto |Sistema de origen de datos actual de hello - Azure |
| ResourceId |Texto |Este campo representa el id. de recurso para el que se están recopilando datos; muestra el id. de recurso del almacén de Recovery Services |
| SubscriptionId |Texto |Este campo representa el identificador de la suscripción de recursos hello (almacén RS) para el que se está recopilando datos |
| ResourceGroup |Texto |Este campo representa el grupo de recursos del recurso de hello (almacén RS) para el que se está recopilando datos |
| ResourceProvider |Texto |Este campo representa el proveedor de recursos de hello para el que se están recopilando datos - Microsoft.RecoveryServices |
| ResourceType |Texto |Este campo representa el tipo de recurso de hello para el que se están recopilando datos - almacenes |

### <a name="storage"></a>Storage
Esta tabla proporciona detalles acerca de los campos relacionados con el almacenamiento.

| Campo | Tipo de datos | Descripción |
| --- | --- | --- |
| CloudStorageInBytes_s |Número decimal |Almacenamiento de copia de seguridad en la nube utilizado por las copias de seguridad, calculados basándose en el último valor |
| ProtectedInstances_s |Número decimal |Número de instancias protegidas que se utilizan para calcular el almacenamiento de front-end en la facturación; se calcula en función del valor más reciente |
| EventName_s |Texto |Este campo representa el nombre de este evento; es siempre AzureBackupCentralReport |
| SchemaVersion_s |Texto |Este campo indica la versión actual del esquema de hello, resulta **V1** |
| State_s |Texto |Estado actual del objeto de almacenamiento de hello, por ejemplo, activo, eliminado |
| BackupManagementType_s |Texto |Tipo de proveedor para realizar la copia de seguridad, por ejemplo, IaaSVM, toowhich FileFolder este almacenamiento pertenece demasiado|
| nombreOperación |Texto |Este campo representa el nombre de la operación actual de hello - almacenamiento |
| Categoría |Texto |Este campo representa la categoría de datos de diagnóstico que se insertan tooLog análisis, entonces se AzureBackupReport |
| Recurso |Texto |Se trata de recursos de hello para el que se está recopilando datos, muestra el nombre del almacén de servicios de recuperación |
| ProtectedServerUniqueId_s |Texto |Identificador único de Hola protegido para el que se calcula el almacenamiento de servidor |
| VaultUniqueId_s |Texto |Identificador único del almacén de hello para el almacenamiento se calcula |
| SourceSystem |Texto |Sistema de origen de datos actual de hello - Azure |
| ResourceId |Texto |Este campo representa el id. de recurso para el que se están recopilando datos; muestra el id. de recurso del almacén de Recovery Services |
| SubscriptionId |Texto |Este campo representa el identificador de la suscripción de recursos hello (almacén RS) para el que se está recopilando datos |
| ResourceGroup |Texto |Este campo representa el grupo de recursos del recurso de hello (almacén RS) para el que se está recopilando datos |
| ResourceProvider |Texto |Este campo representa el proveedor de recursos de hello para el que se están recopilando datos - Microsoft.RecoveryServices |
| ResourceType |Texto |Este representse campo tipo de recurso de hello para el que se están recopilando datos - almacenes |

### <a name="vault"></a>Almacén
Esta tabla proporciona detalles acerca de los campos relacionados con el almacén.

| Campo | Tipo de datos | Descripción |
| --- | --- | --- |
| EventName_s |Texto |Este campo representa el nombre de este evento; es siempre AzureBackupCentralReport |
| SchemaVersion_s |Texto |Este campo indica la versión actual del esquema de hello, resulta **V1** |
| State_s |Texto |Estado actual del objeto de almacén de hello, por ejemplo, activo, eliminado |
| nombreOperación |Texto |Este campo representa el nombre de la operación actual de hello - almacén |
| Categoría |Texto |Este campo representa la categoría de datos de diagnóstico que se insertan tooLog análisis, entonces se AzureBackupReport |
| Recurso |Texto |Se trata de recursos de hello para el que se está recopilando datos, muestra el nombre del almacén de servicios de recuperación |
| VaultUniqueId_s |Texto |Identificador único del almacén de Hola |
| VaultName_s |Texto |Nombre de almacén de Hola |
| AzureDataCenter_s |Texto |Centro de datos donde se encuentra el almacén |
| StorageReplicationType_s |Texto |Tipo de replicación de almacenamiento para el almacén de hello, por ejemplo, GeoRedundant |
| SourceSystem |Texto |Sistema de origen de datos actual de hello - Azure |
| ResourceId |Texto |Este campo representa el id. de recurso para el que se están recopilando datos; muestra el id. de recurso del almacén de Recovery Services |
| SubscriptionId |Texto |Este campo representa el identificador de la suscripción de recursos hello (almacén RS) para el que se está recopilando datos |
| ResourceGroup |Texto |Este campo representa el grupo de recursos del recurso de hello (almacén RS) para el que se está recopilando datos |
| ResourceProvider |Texto |Este campo representa el proveedor de recursos de hello para el que se están recopilando datos - Microsoft.RecoveryServices |
| ResourceType |Texto |Este campo representa el tipo de recurso de hello para el que se están recopilando datos - almacenes |

## <a name="next-steps"></a>Pasos siguientes
Cuando revise el modelo de datos de Hola para crear informes de copia de seguridad de Azure, puede iniciar [crear panel](../log-analytics/log-analytics-dashboards.md) de análisis de registros y OMS.
