---
title: modelo de aaaData de copia de seguridad de Azure
description: "En este artículo se explican los detalles del modelo de datos de Power BI para los informes de Azure Backup."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 0767c330-690d-474d-85a6-aa8ddc410bb2
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/26/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5e3e7ca13c7a3f007c206bd56b8753166a2c264b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="data-model-for-azure-backup-reports"></a>Modelo de datos para informes de Azure Backup
Este artículo describe el modelo de datos de Power BI Hola utilizado para crear informes de copia de seguridad de Azure. Con este modelo de datos, puede filtrar los informes existentes en función de los campos correspondientes y más importante aún, crear sus propios informes mediante el uso de tablas y campos en el modelo de Hola. 

## <a name="creating-new-reports-in-power-bi"></a>Creación de informes nuevos en Power BI
Power BI proporciona características de personalización que puede usar [crear informes mediante el modelo de datos de hello](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/).

## <a name="using-azure-backup-data-model"></a>Uso del modelo de datos de Azure Backup
Puede usar Hola siguiendo los campos que se proporciona como parte de los datos de hello toocreate informes de modelo y personalizar informes existentes.

### <a name="alert"></a>Alerta
Esta tabla proporciona campos y agregaciones básicos en diversos campos relacionados de la alerta.

| Campo | Tipo de datos | Descripción |
| --- | --- | --- |
| #AlertsCreatedInPeriod |Número entero |Número de alertas creadas en el período seleccionado |
| %ActiveAlertsCreatedInPeriod |Porcentaje |Porcentaje de alertas activas en el período seleccionado |
| %CriticalAlertsCreatedInPeriod |Porcentaje |Porcentaje de alertas críticas en el período seleccionado |
| AlertOccurenceDate |Date |Fecha de creación de la alerta |
| AlertSeverity |Texto |Gravedad de alerta de Hola por ejemplo, crítico |
| AlertStatus |Texto |Estado de alerta de Hola por ejemplo, activo |
| AlertType |Texto |Tipo de alerta de hello generado por ejemplo, copia de seguridad |
| AlertUniqueId |Texto |Identificador único de hello generó la alerta |
| AsOnDateTime |Fecha y hora |Hora de la fila seleccionada de Hola de actualización más reciente |
| AvgResolutionTimeInMinsForAlertsCreatedInPeriod |Número decimal |Alerta de tooresolve de promedio de tiempo (en minutos) durante el período de tiempo seleccionado |
| EntityState |Texto |Estado actual del objeto de alerta de Hola por ejemplo, activo, eliminado |

### <a name="backup-item"></a>Elemento de copia de seguridad
Esta tabla proporciona campos y agregaciones básicos en diversos campos relacionados con el elemento de copia de seguridad.

| Campo | Tipo de datos | Descripción |
| --- | --- | --- |
| #BackupItems |Número entero |Número de elementos de copia de seguridad |
| #UnprotectedBackupItems |Número entero |Número de elementos de copia de seguridad detenidos para su protección o configurados para que se realicen copias de seguridad, pero las copias de seguridad no se han iniciado|
| AsOnDateTime |Fecha y hora |Hora de la fila seleccionada de Hola de actualización más reciente |
| BackupItemFriendlyName |Texto |Nombre descriptivo del elemento de copia de seguridad |
| BackupItemId |Texto |Identificador de elemento de copia de seguridad |
| BackupItemName |Texto |Nombre de elemento de copia de seguridad |
| BackupItemType |Texto |Tipo de elemento de copia de seguridad, por ejemplo, VM o FileFolder |
| EntityState |Texto |Estado actual del objeto de elemento de copia de seguridad de Hola por ejemplo, activo, eliminado |
| LastBackupDateTime |Fecha y hora |Hora de la última copia de seguridad del elemento de copia de seguridad seleccionado |
| LastBackupState |Texto |Estado de la última copia de seguridad del elemento de copia de seguridad seleccionado, por ejemplo, Successful o Failed |
| LastSuccessfulBackupDateTime |Fecha y hora |Hora de última copia de seguridad correcta del elemento de copia de seguridad seleccionado |
| ProtectionState |Texto |Estado de protección actual del elemento de copia de seguridad de Hola por ejemplo, Protected, ProtectionStopped |

### <a name="calendar"></a>Calendario
Esta tabla proporciona detalles acerca de los campos relacionados con el calendario.

| Campo | Tipo de datos | Descripción |
| --- | --- | --- |
| Fecha |Fecha |Fecha seleccionada para filtrar datos |
| DateKey |Texto |Clave única para cada elemento de fecha |
| DayDiff |Número decimal |Diferencia en el día al filtrar datos, por ejemplo, 0 indican los datos del día actual, -1 indica los datos de un día anterior y 0 y -1 indican los datos del día actual y del anterior  |
| Mes |Texto |Mes del año de hello seleccionado para filtrar datos, empieza el primer día mes y termina el 31 días |
| MonthDate | Date |Fecha en el mes de hello cuando finaliza el mes, seleccionado para filtrar datos |
| MonthDiff |Número decimal |Diferencia en el mes al filtrar datos, por ejemplo, 0 indican los datos del mes actual, -1 indica los datos de un mes anterior y 0 y -1 indican los datos del mes actual y del anterior |
| Semana |Texto |Semana seleccionada para filtrar los datos; la semana comienza el domingo y termina el sábado |
| WeekDate |Date |Fecha de la semana de hello cuando finaliza la semana, seleccionado para filtrar datos |
| WeekDiff |Número decimal |Diferencia en la semana al filtrar datos, por ejemplo, 0 indican los datos de la semana actual, -1 indica los datos de una semana anterior y 0 y -1 indican los datos de la semana actual y de la anterior |
| Year |Texto |Año natural para filtrar datos |
| YearDate |Date |Fecha del año de hello cuando finaliza el año, seleccionado para filtrar datos |

### <a name="job"></a>Trabajo
Esta tabla proporciona campos y agregaciones básicos en diversos campos relacionados con el trabajo.

| Campo | Tipo de datos | Descripción |
| --- | --- | --- |
| #JobsCreatedInPeriod |Número entero |Número de trabajos creados en hello período de tiempo seleccionado |
| %FailuresForJobsCreatedInPeriod |Porcentaje |Porcentaje de errores en el período de tiempo seleccionado de Hola general de los trabajos |
| 80thPercentileDataTransferredInMBForBackupJobsCreatedInPeriod |Número decimal |valor de percentil 80 de los datos transferidos en MB para **copia de seguridad** trabajos creados en hello período de tiempo seleccionado |
| AsOnDateTime |Fecha y hora |Hora de la fila seleccionada de Hola de actualización más reciente |
| AvgBackupDurationInMinsForJobsCreatedInPeriod |Número decimal |Tiempo medio, en minutos, de los trabajos de **copia de seguridad completados** creados en el período seleccionado |
| AvgRestoreDurationInMinsForJobsCreatedInPeriod |Número decimal |Tiempo medio, en minutos, de los trabajos de **restauración completados** creados en el período seleccionado |
| BackupStorageDestination |Texto |Destino de almacenamiento de almacenamiento de copias de seguridad, por ejemplo, Cloud o Disk  |
| EntityState |Texto |Estado actual del objeto de trabajo de Hola por ejemplo, activo, eliminado |
| JobFailureCode |Texto |Cadena del código de error por el que produjo el error del trabajo |
| JobOperation |Texto |Operación para la que se ejecuta el trabajo, por ejemplo, Backup, Restore o Configure Backup |
| JobStartDate |Fecha |Fecha en que comenzó la ejecución del trabajo |
| JobStartTime |Hora |Hora en que comenzó la ejecución del trabajo |
| Estado del trabajo |Texto |Estado de hello terminan por ejemplo, trabajo completado, no se pudo |
| JobUniqueId |Texto |Trabajo de hello tooidentify de Id. único |

### <a name="policy"></a>Directiva
Esta tabla proporciona campos y agregaciones básicos en diversos campos relacionados con la directiva.

| Campo | Tipo de datos | Descripción |
| --- | --- | --- |
| #Directivas |Número entero |Número de directivas de copia de seguridad que existen en el sistema de Hola |
| #PoliciesInUse |Número entero |Número de directivas que se usan actualmente para configurar copias de seguridad |
| AsOnDateTime |Fecha y hora |Hora de la fila seleccionada de Hola de actualización más reciente |
| BackupDaysOfTheWeek |Texto |Días de la semana de hello cuando se hayan programado las copias de seguridad |
| BackupFrequency |Texto |Frecuencia con la que se ejecutan las copias de seguridad, por ejemplo, a diario o semanalmente |
| BackupTimes |Texto |Fecha y hora en que se programan las copias de seguridad |
| DailyRetentionDuration |Número entero |Duración de retención total de las copias de seguridad configuradas, en días |
| DailyRetentionTimes |Texto |Fecha y hora en que se configuró la retención diaria |
| EntityState |Texto |Estado actual del objeto de directiva de Hola por ejemplo, activo, eliminado |
| MonthlyRetentionDaysOfTheMonth |Texto |Fechas del mes de hello seleccionado para la retención mensual |
| MonthlyRetentionDaysOfTheWeek |Texto |Días de la semana de hello seleccionado para la retención mensual |
| MonthlyRetentionDuration |Número decimal |Duración de retención total de las copias de seguridad configuradas, en meses |
| MonthlyRetentionFormat |Texto |Tipo de configuración para la retención mensual ,por ejemplo, diariamente si se basa en día, semanalmente si se basa en semana |
| MonthlyRetentionTimes |Texto |Fecha y hora en que se ha configurado la retención mensual |
| MonthlyRetentionWeeksOfTheMonth |Texto |Semanas del mes de hello cuando retención mensual es habían configurado por ejemplo, primero, último etcetera. |
| PolicyName |Texto |Nombre de directiva de hello definida |
| PolicyUniqueId |Texto |Directiva de hello tooidentify de Id. único |
| RetentionType |Texto |Tipo de directiva de retención, por ejemplo, Daily, Weekly, Monthly, Yearly |
| WeeklyRetentionDaysOfTheWeek |Texto |Días de la semana de hello seleccionado para la retención semanal |
| WeeklyRetentionDuration |Número decimal |Duración total de la retención semanal de las copias de seguridad configuradas, en semanas |
| WeeklyRetentionTimes |Texto |Fecha y hora en que se ha configurado la retención semanal |
| YearlyRetentionDaysOfTheMonth |Texto |Fechas del mes de hello seleccionado para retención anual |
| YearlyRetentionDaysOfTheWeek |Texto |Días de la semana de hello seleccionado para retención anual |
| YearlyRetentionDuration |Número decimal |Duración total de la retención de las copias de seguridad configuradas, en años |
| YearlyRetentionFormat |Texto |Tipo de configuración para la retención anual ,por ejemplo, diariamente si se basa en día, semanalmente si se basa en semana |
| YearlyRetentionMonthsOfTheYear |Texto |Meses del año de hello seleccionado para retención anual |
| YearlyRetentionTimes |Texto |Fecha y hora en que se ha configurado la retención anual |
| YearlyRetentionWeeksOfTheMonth |Texto |Semanas del mes de hello cuando retención anual es habían configurado por ejemplo, primero, último etcetera. |

### <a name="protected-server"></a>Servidor protegido
Esta tabla proporciona campos y agregaciones básicos en diversos campos relacionados con el servidor protegido.

| Campo | Tipo de datos | Descripción |
| --- | --- | --- |
| #ProtectedServers |Número entero |Número de servidores protegidos |
| AsOnDateTime |Fecha y hora |Hora de la fila seleccionada de Hola de actualización más reciente |
| AzureBackupAgentOSType |Texto |Tipo de sistema operativo de Azure Backup Agent |
| AzureBackupAgentOSVersion |Texto |Versión del sistema operativo de Azure Backup Agent |
| AzureBackupAgentUpdateDate |Texto |Fecha de actualización de Azure Backup Agent |
| AzureBackupAgentVersion |Texto |Número de versión de Azure Backup Agent |
| BackupManagementType |Texto |Tipo de proveedor para realizar la copia de seguridad, por ejemplo, IaaSVM o FileFolder |
| EntityState |Texto |Estado actual del objeto de servidor protegido de Hola por ejemplo, activo, eliminado |
| ProtectedServerFriendlyName |Texto |Nombre descriptivo del servidor protegido |
| ProtectedServerName |Texto |Nombre del servidor protegido |
| ProtectedServerType |Texto |Tipo de servidor protegido del que se realiza la copia de seguridad, por ejemplo, IaaSVMContainer |
| ProtectedServerName |Texto |Nombre de elemento de copia de seguridad de servidor protegido toowhich pertenece |
| RegisteredContainerId |Texto |Identificador de contenedor registrado para copia de seguridad |

### <a name="storage"></a>Almacenamiento
Esta tabla proporciona campos y agregaciones básicos en diversos campos relacionados con el almacenamiento.

| Campo | Tipo de datos | Descripción |
| --- | --- | --- |
| #ProtectedInstances |Número decimal |Número de instancias protegidas que se utilizan para calcular el almacenamiento de front-end en la facturación; se calcula en función del valor más reciente del tiempo seleccionado |
| AsOnDateTime |Fecha y hora |Hora de la fila seleccionada de Hola de actualización más reciente |
| CloudStorageInMB |Número decimal |Almacenamiento de copia de seguridad en la nube utilizado por las copias de seguridad, calculados basándose en el último valor de tiempo seleccionado |
| EntityState |Texto |Estado actual del objeto de Hola por ejemplo, activo, eliminado |
| LastUpdatedDate |Date |Fecha de última actualización de la fila seleccionada |

### <a name="time"></a>Hora
Esta tabla proporciona detalles acerca de los campos relacionados con el tiempo.

| Campo | Tipo de datos | Descripción |
| --- | --- | --- |
| Hora |Hora |Hora del día de hello, por ejemplo, 1:00:00 P.M. |
| HourNumber |Número decimal |Número de horas en el día de hello 13.00, por ejemplo, |
| Minuto |Número decimal |Minuto de la hora de Hola |
| PeriodOfTheDay |Texto |Ranura de período de tiempo en día Hola por ejemplo, 12-3 A.M. |
| Hora |Hora |Hora del día de hello, por ejemplo, 12:00:01 AM |
| TimeKey |Texto |Tiempo de toorepresent del valor de clave |

### <a name="vault"></a>Almacén
Esta tabla proporciona campos y agregaciones básicos en diversos campos relacionados con el almacén.

| Campo | Tipo de datos | Descripción |
| --- | --- | --- |
| #Vaults |Número entero |Número de almacenes |
| AsOnDateTime |Fecha y hora |Hora de la fila seleccionada de Hola de actualización más reciente |
| AzureDataCenter |Texto |Centro de datos donde se encuentra el almacén |
| EntityState |Texto |Estado actual del objeto de almacén de Hola por ejemplo, activo, eliminado |
| StorageReplicationType |Texto |Tipo de replicación de almacenamiento para el almacén de hello GeoRedundant por ejemplo, |
| SubscriptionId |Texto |Id. de suscripción de cliente de hello seleccionado para la generación de informes |
| VaultName |Texto |Nombre de almacén de Hola |
| VaultTags |Texto |Las etiquetas asociadas toohello almacén |

## <a name="next-steps"></a>Pasos siguientes
Una vez que revisar el modelo de datos de Hola para crear informes de copia de seguridad de Azure, consulte Hola siguientes artículos para obtener más información sobre cómo crear y ver informes en Power BI.

* [Creación de un informe de Power BI nuevo mediante la importación de un conjunto de datos](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/)
* [Filtros y resaltado en informes de Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-about-filters-and-highlighting-in-reports/)
