---
title: aaaView actividad de Azure registra recursos toomonitor | Documentos de Microsoft
description: Actividad de uso hello registra errores y las acciones del usuario tooreview. Muestra PowerShell del Portal de Azure, CLI de Azure CLI y REST.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fcdb3125-13ce-4c3b-9087-f514c5e41e73
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: tomfitz
ms.openlocfilehash: 8430ed2a9c1dfe5f13423a55d358e590b0facb22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="view-activity-logs-tooaudit-actions-on-resources"></a>Ver la actividad registra acciones de tooaudit en recursos
Mediante los registros de actividad, puede determinar:

* las operaciones que se realizaron en los recursos de hello en su suscripción
* quién inició la operación de hello (aunque las operaciones iniciadas por un servicio back-end no devuelven un usuario como autor de llamada de hello)
* Cuando se ha producido la operación de Hola
* estado de Hola de operación de Hola
* valores de Hello de otras propiedades que pueden ayudarle a investigación operación Hola

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

Puede recuperar información de los registros de actividad de Hola a través del portal de hello, PowerShell, CLI de Azure, API de REST de visión, o [biblioteca .NET de visión](https://www.nuget.org/packages/Microsoft.Azure.Insights/).

## <a name="portal"></a>Portal
1. registros de actividad de hello tooview a través del portal de hello, seleccione **Monitor**.
   
    ![seleccionar registro de actividad](./media/resource-group-audit/select-monitor.png)

   O bien, tooautomatically filtrar el registro de actividad de Hola para un determinado recurso o grupo de recursos, seleccione **registro de actividad** de esa hoja de recursos. Tenga en cuenta que este registro de actividad de Hola se filtra automáticamente por recurso Hola seleccionado.
   
    ![filtrar por recurso](./media/resource-group-audit/filtered-by-resource.png)
2. Hola **registro de actividad** hoja, verá un resumen de las operaciones recientes.
   
    ![mostrar acciones](./media/resource-group-audit/audit-summary.png)
3. número de hello toorestrict de operaciones que se muestra, seleccione las distintas condiciones. Por ejemplo, hello siguiente imagen muestra hello **Timespan** y **evento iniciado por** campos cambiaron las acciones de hello tooview realizadas por un usuario determinado o una aplicación para hello mes pasado. Seleccione **aplicar** tooview resultados de saludo de la consulta.
   
    ![establecer opciones de filtro](./media/resource-group-audit/set-filter.png)

4. Si necesita toorun consulta de Hola de nuevo más tarde, seleccione **guardar** y asigne un nombre de consulta de Hola.
   
    ![guardar consulta](./media/resource-group-audit/save-query.png)
5. tooquickly al ejecutar una consulta, puede seleccionar uno de consultas integradas de hello, como implementaciones con error.

    ![seleccionar consulta](./media/resource-group-audit/select-quick-query.png)

   consulta seleccionada Hola establece automáticamente los valores de filtro de hello necesario.

    ![ver errores de implementación](./media/resource-group-audit/view-failed-deployment.png)   

6. Seleccione uno de hello operaciones toosee un resumen del evento Hola.

    ![ver operación](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a>PowerShell
1. entradas del registro tooretrieve, ejecute hello **Get AzureRmLog** comando. Proporcionar la lista de parámetros adicionales toofilter Hola de entradas. Si no especifica una hora inicial y final, se devuelven las entradas de hello última hora. Por ejemplo, las operaciones de Hola de tooretrieve de un grupo de recursos durante la última hora de hello ejecutan:

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    Hola de ejemplo siguiente muestra cómo actividad de hello toouse registro operaciones tooresearch realizadas durante un tiempo especificado. Hola se especifican las fechas de inicio y finalización en un formato de fecha.

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    O bien, puede usar funciones toospecify Hola fecha intervalo de fechas, como Hola últimos 14 días.
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. Según la hora de inicio de Hola que especifique, comandos anteriores Hola pueden devolver una lista larga de operaciones para el grupo de recursos de Hola. Puede filtrar los resultados de Hola para lo está buscando al proporcionar criterios de búsqueda. Por ejemplo, si está tratando de tooresearch cómo una aplicación web se detiene, podría ejecutar Hola siguiente comando:

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    En este ejemplo se muestra que someone@contoso.com ha realizado una acción de detención. 

  ```powershell 
  Authorization     :
  Scope     : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Action    : Microsoft.Web/sites/stop/action
  Role      : Subscription Admin
  Condition :
  Caller            : someone@contoso.com
  CorrelationId     : 84beae59-92aa-4662-a6fc-b6fecc0ff8da
  EventSource       : Administrative
  EventTimestamp    : 8/28/2015 4:08:18 PM
  OperationName     : Microsoft.Web/sites/stop/action
  ResourceGroupName : ExampleGroup
  ResourceId        : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Status            : Succeeded
  SubscriptionId    : xxxxx
  SubStatus         : OK
  ```

3. Puede buscar las acciones de hello realizadas por un usuario determinado, incluso para un grupo de recursos que ya no existe.

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. Puede filtrar por las operaciones con errores.

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. Se puede concentrar en un error examinando el mensaje de estado de Hola para esa entrada.
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    Que devuelve:
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a>CLI de Azure
* las entradas del registro tooretrieve ejecutar hello **mostrar de registro del grupo de azure** comando.

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a>API de REST
operaciones de REST de Hola para trabajar con el registro de actividad de hello forman parte del programa Hola a [API de REST de visión](https://msdn.microsoft.com/library/azure/dn931943.aspx). eventos de registro de actividad de tooretrieve, consulte [lista de los eventos de administración de hello en una suscripción](https://msdn.microsoft.com/library/azure/dn931934.aspx).

## <a name="next-steps"></a>Pasos siguientes
* Registros de actividad de Azure pueden utilizarse con Power BI toogain mayor información útil sobre las acciones de hello en su suscripción. Consulte [View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/)(Consulta y análisis de registros de auditoría de Azure en Power BI y más).
* toolearn acerca de cómo establecer directivas de seguridad, consulte [el Control de acceso basado en roles de Azure](../active-directory/role-based-access-control-configure.md).
* toolearn acerca de los comandos de Hola para ver las operaciones de implementación, consulte [ver las operaciones de implementación](resource-manager-deployment-operations.md).
* toolearn tooprevent eliminaciones en un recurso para todos los usuarios, vea [bloquear los recursos con el Administrador de recursos de Azure](resource-group-lock-resources.md).

