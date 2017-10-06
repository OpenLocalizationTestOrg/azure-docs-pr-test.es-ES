---
title: informe de aaaAccess - RBAC de Azure | Documentos de Microsoft
description: "Generar un informe que enumera todos los cambios en acceso tooyour suscripciones de Azure con Control de acceso basado en roles a través de hello últimos 90 días."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 2bc68595-145e-4de3-8b71-3a21890d13d9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9ad85d3d8e66ce167032638a35e4afffb46d3892
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-access-report-for-role-based-access-control"></a>Creación de un informe de acceso para el control de acceso basado en roles
Siempre que alguien concede o revoca el acceso dentro de sus suscripciones, se registran los cambios de hello en los eventos de Azure. Puede crear toosee de informes de historial de cambios de acceso todos los cambios de hello últimos 90 días.

## <a name="create-a-report-with-azure-powershell"></a>Creación de un informe con Azure PowerShell
toocreate un acceso cambiar el informe de historial en PowerShell, use hello [Get AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) comando.

Cuando se llama a este comando, puede especificar qué propiedad de asignaciones de Hola que desee enumerados, incluyendo Hola siguiente:

| Propiedad | Description |
| --- | --- |
| **Acción** |Si se ha concedido o revocado el acceso. |
| **Autor de llamada** |Cambiar propietario Hola responsable del acceso de Hola |
| **PrincipalId** | Identificador único del usuario de hello, grupo o aplicación que se ha asignado el rol de Hola de Hola |
| **PrincipalName** |nombre de Hola de hello usuario, grupo o aplicación |
| **PrincipalType** |Si la asignación Hola era una aplicación, grupo o usuario |
| **RoleDefinitionId** |Hola GUID de rol de Hola que se ha concedido o revocado |
| **RoleName** |función Hello que se ha concedido o revocado |
| **Ámbito** | Identificador único de Hola de suscripción de hello, el grupo de recursos o el recurso que Hola asignación se aplica demasiado| 
| **ScopeName** |nombre de Hola de suscripción de hello, el grupo de recursos o el recurso |
| **ScopeType** |Si era la asignación de hello en ámbito de recursos, grupo de recursos o suscripción de Hola |
| **Timestamp** |Hola fecha y hora en que el acceso se ha cambiado |

Este comando de ejemplo enumera todos los cambios de acceso en la suscripción de Hola para hello últimos siete días:

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get:AzureRMAuthorizationChangeLog (captura de pantalla)](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a>Creación de un informe con la CLI de Azure
toocreate un informe de historial de cambios de acceso en hello Azure interfaz de línea de comandos (CLI), usar hello `azure role assignment changelog list` comando.

## <a name="export-tooa-spreadsheet"></a>Hoja de cálculo de exportación tooa
toosave Hola informe o manipular los datos de hello, el acceso de exportación Hola los cambios en un archivo .csv. A continuación, puede ver informes de hello en una hoja de cálculo para su revisión.

![Changelog visto como una hoja de cálculo ( captura de pantalla)](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a>Pasos siguientes
* Uso de [roles personalizados en RBAC de Azure](role-based-access-control-custom-roles.md)
* Obtenga información acerca de cómo toomanage [RBAC de Azure con powershell](role-based-access-control-manage-access-powershell.md)

