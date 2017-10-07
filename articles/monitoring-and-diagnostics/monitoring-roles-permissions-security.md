---
title: aaaGet a trabajar con roles, permisos y seguridad con el Monitor de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Azure Monitor roles integrados y permisos toorestrict tener acceso a recursos de toomonitoring."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 2686e53b-72f0-4312-bcd3-3dc1b4a9b912
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: johnkem
ms.openlocfilehash: 44fdf2a697050309480dfc164ebab51445b19bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-roles-permissions-and-security-with-azure-monitor"></a>Introducción a roles, permisos y seguridad con Azure Monitor
Muchos equipos necesitan toostrictly regulan toomonitoring acceder a los datos y la configuración. Por ejemplo, si tiene los miembros del equipo que trabajan en exclusivamente de supervisión (ingenieros de soporte técnico, ingenieros de devops) o si usa un proveedor de servicios administrados, puede que desee toogrant acceso tooonly datos de supervisión al restringir su toocreate de capacidad, modificar, o eliminar los recursos. Este artículo muestra cómo tooquickly aplicar un supervisión RBAC rol tooa usuario integradas en Azure o crear sus propios roles personalizados para un usuario que necesita permisos de supervisión limitados. , A continuación, describe las consideraciones de seguridad para los recursos relacionados con el Monitor de Azure y cómo puede limitar el acceso a los datos toohello contienen.

## <a name="built-in-monitoring-roles"></a>Roles de supervisión integrados
Funciones integradas del Monitor de Azure están diseñadas toohelp límite acceso tooresources en una suscripción mientras aún habilita los responsables de supervisar la infraestructura tooobtain y configurar los datos de Hola que necesitan. Azure Monitor proporciona dos roles de fábrica: un lector de supervisión y un colaborador de supervisión.

### <a name="monitoring-reader"></a>Lector de supervisión
Personas asignado el rol de lector de supervisión de hello pueden ver todos los datos de supervisión en una suscripción, pero no se puede modificar cualquier recurso o editar los recursos de configuración relacionados toomonitoring. Esta función es adecuada para los usuarios de una organización, por ejemplo, ingenieros de soporte técnico u operaciones que necesitan toobe capaz de:

* Ver los paneles de supervisión en el portal de Hola y crear sus propios paneles de supervisión privadas.
* Consultar las métricas con hello [API de REST de Azure Monitor](https://msdn.microsoft.com/library/azure/dn931930.aspx), [cmdlets de PowerShell](insights-powershell-samples.md), o [multiplataforma CLI](insights-cli-samples.md).
* Consulta Hola mediante el portal de hello, API de REST de Monitor de Azure, cmdlets de PowerShell o CLI multiplataforma de registro de actividad.
* Hola de vista [configuración de diagnóstico](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) para un recurso.
* Hola de vista [registro perfil](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) para una suscripción.
* Consultar la configuración de escalado automático.
* Consultar la configuración y actividad de alertas.
* Acceder a datos de Application Insights y ver los datos en AI Analytics.
* Buscar datos del área de trabajo de análisis de registros (OMS) junto con datos de uso para el área de trabajo de Hola.
* Ver grupos de administración de Log Analytics (OMS).
* Recuperar el esquema de búsqueda de hello Log Analytics (OMS).
* Enumerar los Intelligence Pack de Log Analytics (OMS).
* Recuperar y ejecutar las búsquedas guardadas en Log Analytics (OMS).
* Recuperar la configuración de almacenamiento de hello Log Analytics (OMS).

> [!NOTE]
> Este rol no le otorga acceso de lectura toolog datos que se ha transmitido tooan concentrador de eventos o almacenada en una cuenta de almacenamiento. [Vea más adelante](#security-considerations-for-monitoring-data) para obtener información acerca de cómo configurar el acceso a los recursos de toothese.
> 
> 

### <a name="monitoring-contributor"></a>Colaborador de supervisión
Personas asignadas Hola supervisión Colaborador rol puede ver todos los datos de supervisión en una suscripción y crear o modificar la configuración de supervisión, pero no se puede modificar ningún otro recurso. Esta función es un supraconjunto de rol de lector de supervisión de Hola y es adecuada para los miembros del equipo de supervisión o proveedores de servicios administrados que además toohello permisos anteriores, también se deben toobe capaz de la organización:

* Publicar paneles de supervisión como un panel compartido.
* Determinar la [configuración de diagnóstico](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) de un recurso.*
* Conjunto hello [registro perfil](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) para un suscripción.* como
* Definir la configuración y actividad de alertas.
* Crear componentes y pruebas web de Application Insights.
* Mostrar las claves compartidas del área de trabajo de Log Analytics (OMS).
* Habilitar o deshabilitar Intelligence Pack de Log Analytics (OMS).
* Crear y eliminar y ejecutar las búsquedas guardadas en Log Analytics (OMS).
* Crear y eliminar la configuración de almacenamiento de hello Log Analytics (OMS).

* usuario también por separado debe tener permiso de ListKeys en tooset de recursos (almacenamiento cuenta o evento de concentrador espacio de nombres) de destino de hello un perfil de registro o la configuración de diagnóstico.

> [!NOTE]
> Este rol no le otorga acceso de lectura toolog datos que se ha transmitido tooan concentrador de eventos o almacenada en una cuenta de almacenamiento. [Vea más adelante](#security-considerations-for-monitoring-data) para obtener información acerca de cómo configurar el acceso a los recursos de toothese.
> 
> 

## <a name="monitoring-permissions-and-custom-rbac-roles"></a>Roles RBAC personalizados y permisos de supervisión
Si Hola por encima de funciones integradas no satisface necesidades específicas de Hola de su equipo, puede [crear un rol personalizado de RBAC](../active-directory/role-based-access-control-custom-roles.md) con más permisos granulares. A continuación se muestran Hola operaciones comunes de Azure Monitor RBAC con sus descripciones.

| Operación | Description |
| --- | --- |
| Microsoft.Insights/AlertRules/[Read, Write, Delete] |Reglas de alerta de lectura, escritura y eliminación. |
| Microsoft.Insights/AlertRules/Incidents/Read |Lista de incidentes (historial de regla de alerta de Hola se desencadena) para las reglas de alerta. Esto solo aplica toohello portal. |
| Microsoft.Insights/AutoscaleSettings/[Read, Write, Delete] |Configuración de escalado automático de lectura, escritura y eliminación. |
| Microsoft.Insights/DiagnosticSettings/[Read, Write, Delete] |Configuración de diagnóstico de lectura, escritura y eliminación. |
| Microsoft.Insights/eventtypes/digestevents/Read |Este permiso es necesario para los usuarios que necesitan obtener acceso a los registros de tooActivity mediante el portal de Hola. |
| Microsoft.Insights/eventtypes/values/Read |Enumerar eventos del registro de actividades (eventos de administración) de una suscripción. Este permiso es aplicable tooboth mediante programación y acceso al portal toohello registro de actividad. |
| Microsoft.Insights/LogDefinitions/Read |Este permiso es necesario para los usuarios que necesitan obtener acceso a los registros de tooActivity mediante el portal de Hola. |
| Microsoft.Insights/MetricDefinitions/Read |Leer definiciones de métrica (lista de tipos de métricas disponibles para un recurso). |
| Microsoft.Insights/Metrics/Read |Leer las métricas de un recurso. |

> [!NOTE]
> Obtener acceso a tooalerts, configuración de diagnóstico y métricas para un recurso que requiere que el usuario hello tiene tipo de recurso de toohello de acceso de lectura y el ámbito de ese recurso. Crear ("escritura") un perfil de configuración o de registro de diagnóstico que archivos tooa centros de almacenamiento cuenta o secuencias tooevent requiere hello tooalso de usuario tiene permiso de ListKeys de recurso de destino de Hola.
> 
> 

Por ejemplo, mediante Hola por encima de la tabla podría crear un rol RBAC personalizado para un "lector de registro de actividad" similar al siguiente:

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Activity Log Reader"
$role.Description = "Can view activity logs."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Insights/eventtypes/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription")
New-AzureRmRoleDefinition -Role $role 
```

## <a name="security-considerations-for-monitoring-data"></a>Consideraciones de seguridad para datos de supervisión
Los datos de supervisión, en particular los archivos de registro, pueden obtener información confidencial, como los nombres de usuario o las direcciones IP. Los datos de supervisión de Azure se presentan en tres formatos básicos:

1. Hola registro de actividad, que describe todas las acciones de plano de control en su suscripción de Azure.
2. Los registros de diagnóstico, que son registros emitidos por un recurso.
3. Métricas, que emiten los recursos.

Los tres tipos de datos pueden almacenarse en una cuenta de almacenamiento o en Stream tooEvent concentrador, ambos de los cuales son recursos de Azure de uso generales. Dado que son recursos de uso general, su creación, eliminación o el acceso a ellos constituyen una operación privilegiada que suele estar reservada a un administrador. Se recomienda que utilice Hola seguir prácticas recomendadas para el uso incorrecto de tooprevent de recursos relacionados con la supervisión:

* Utilizar una cuenta de almacenamiento dedicada a datos de supervisión. Si necesita tooseparate datos de supervisión en varias cuentas de almacenamiento, nunca comparten el uso de una cuenta de almacenamiento entre supervisión y datos sin supervisión, este pueden provocar accidentalmente quienes solo necesita tener acceso a los datos de toomonitoring (p. ej. un SIEM terceros) tener acceso a datos de supervisión de toonon.
* Usar nombres de Bus de servicio o un concentrador de eventos única y exclusiva en toda la configuración de diagnóstico para hello mismo motivo como anteriormente.
* Limitar las cuentas de acceso de almacenamiento relacionada con toomonitoring o concentradores de eventos guardándolas en un grupo de recursos independiente, y [utilizar ámbito](../active-directory/role-based-access-control-what-is.md#basics-of-access-management-in-azure) en sus roles supervisión toolimit acceso tooonly ese grupo de recursos.
* Nunca debe conceder permiso de ListKeys de Hola para las cuentas de almacenamiento o en centros de eventos en el ámbito de la suscripción cuando un usuario solo necesita acceder a los datos toomonitoring. En su lugar, asigne estos permisos, usuario toohello en un recurso o grupo de recursos (si tiene un grupo de recursos de supervisión dedicado) ámbito.

### <a name="limiting-access-toomonitoring-related-storage-accounts"></a>Limitar las cuentas de almacenamiento relacionada con el toomonitoring de acceso
Cuando un usuario o una aplicación necesita tener acceso a datos toomonitoring en una cuenta de almacenamiento, debe [generar una SAS de cuenta](https://msdn.microsoft.com/library/azure/mt584140.aspx) Hola cuenta de almacenamiento que contiene los datos de supervisión con el almacenamiento de tooblob de acceso de solo lectura de nivel de servicio. En PowerShell, podría quedar de manera similar a:

```powershell
$context = New-AzureStorageContext -ConnectionString "[connection string for your monitoring Storage Account]"
$token = New-AzureStorageAccountSASToken -ResourceType Service -Service Blob -Permission "rl" -Context $context
```

Puede proporcionar después a entidades de token toohello Hola que necesita tooread desde esa cuenta de almacenamiento, y puede enumerar y leer todos los blobs en esa cuenta de almacenamiento.

Como alternativa, si necesita toocontrol este permiso con RBAC, puede conceder ese Hola entidad permiso Microsoft.Storage/storageAccounts/listkeys/action en dicha cuenta de almacenamiento en particular. Esto es necesario para los usuarios que necesitan toobe puede tooset un diagnóstico configuración o registro perfil tooarchive tooa cuenta de almacenamiento. Por ejemplo, podría crear Hola siguiendo las funciones RBAC personalizado para un usuario o aplicación que solo necesita tooread desde una cuenta de almacenamiento:

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Monitoring Storage Account Reader"
$role.Description = "Can get hello storage account keys for a monitoring storage account."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/storageAccounts/listkeys/action")
$role.Actions.Add("Microsoft.Storage/storageAccounts/Read")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/myMonitoringStorageAccount")
New-AzureRmRoleDefinition -Role $role 
```

> [!WARNING]
> Hola ListKeys permiso permite claves de cuenta de almacenamiento principal y secundaria de hello usuario toolist Hola. Estas claves conceder usuario Hola todos firmados permisos (lectura, escritura, crear blobs y eliminar blobs, etc.) en todos firmados servicios (blob, cola, tabla o archivo) en esa cuenta de almacenamiento. Se recomienda usar una SAS de cuenta, como se ha descrito anteriormente, cuando sea posible.
> 
> 

### <a name="limiting-access-toomonitoring-related-event-hubs"></a>Limitación de los centros de eventos relacionados con el toomonitoring de acceso
Los concentradores de eventos puede ir seguido de un patrón similar, pero primero debe toocreate una regla de autorización de escucha dedicada. Si desea que toogrant acceso tooan aplicación que basta con que los centros de eventos relacionados con el toomonitoring toolisten, Hola siguientes:

1. Crear una directiva de acceso compartido en hello concentradores de eventos que se crearon para la transmisión por secuencias de datos de supervisión con solo las notificaciones de escucha. Esto puede hacerse en el portal de Hola. Por ejemplo, podría llamarlo "monitoringReadOnly." Si es posible, le interesará toogive que directamente clave toohello consumidor y omitir el paso siguiente de saludo.
2. Si el consumidor de hello necesita toobe tooget capaz de hello clave ad-hoc, conceda acción de ListKeys Hola Hola de usuario para ese concentrador de eventos. Esto también es necesario para los usuarios que necesiten toobe capaz tooset una configuración de diagnóstico o centros de tooevent toostream de perfil de registro. Por ejemplo, podría crear una regla de RBAC:
   
   ```powershell
   $role = Get-AzureRmRoleDefinition "Reader"
   $role.Id = $null
   $role.Name = "Monitoring Event Hub Listener"
   $role.Description = "Can get hello key toolisten tooan event hub streaming monitoring data."
   $role.Actions.Clear()
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/authorizationrules/listkeys/action")
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/Read")
   $role.AssignableScopes.Clear()
   $role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.ServiceBus/namespaces/mySBNameSpace")
   New-AzureRmRoleDefinition -Role $role 
   ```

## <a name="next-steps"></a>Pasos siguientes
* [Consulte información sobre RBAC y permisos en Resource Manager](../active-directory/role-based-access-control-what-is.md)
* [Información general de Hola de lectura de la supervisión de Azure](monitoring-overview.md)

