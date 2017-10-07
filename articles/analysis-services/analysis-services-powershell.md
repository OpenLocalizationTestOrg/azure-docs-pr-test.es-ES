---
title: aaaManage Analysis Services con PowerShell de Azure | Documentos de Microsoft
description: "Administración de Azure Analysis Services con PowerShell."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: owend
ms.openlocfilehash: bc4250bf77b5a0d86c1049ee57493bcf2a1f0c1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-analysis-services-with-powershell"></a>Administración de Azure Analysis Services con PowerShell

Este artículo describe PowerShell cmdlets usados tooperform Azure Analysis Services server y base de datos de tareas de administración. 

Tareas de administración del servidor, como la creación o eliminación de un servidor, suspender o reanudar las operaciones del servidor o cambiar el nivel de servicio de hello (nivel) usan cmdlets de Azure Resource Manager (AzureRM). Otras tareas para administrar las bases de datos, como agregar o quitar miembros del rol, el procesamiento o usar cmdlets de creación de particiones que se incluye en Hola mismo módulo de SQL Server que SQL Server Analysis Services.

## <a name="permissions"></a>Permisos
Mayoría de las tareas de PowerShell requiere que tener privilegios de administrador en servidor de Analysis Services de Hola que está administrando. Las tareas programadas de PowerShell son operaciones desatendidas. cuenta de Hello ejecutando programador Hola debe tener privilegios de administrador en el servidor de Analysis Services de Hola. 

Para las operaciones del servidor mediante cmdlets de AzureRm, su cuenta u Hola ejecutando el programador debe pertenecer también toohello el rol de propietario para el recurso de hello en [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md). 

## <a name="server-operations"></a>Operaciones del servidor 
Cmdlets de Azure para Analysis Services se incluyen en hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) módulo del componente. módulos de cmdlets de tooinstall AzureRM, consulte [cmdlets de Azure Resource Manager](/powershell/azure/overview) Hola Galería de PowerShell.

|Cmdlet|Descripción| 
|------------|-----------------| 
|[Export-AzureAnalysisServicesInstance](/powershell/module/azurerm.analysisservices/export-azureanalysisservicesinstancelog)|Exportaciones de registro toofile.| 
|[Get-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/get-azurermanalysisservicesserver)|Obtiene los detalles de una instancia del servidor.|  
|[New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver)|Crea una instancia de servidor.|
|[Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/remove-azurermanalysisservicesserver)|Quita una instancia de servidor.|  
|[Suspend-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/suspend-azurermanalysisservicesserver)|Suspende una instancia de servidor.| 
|[Resume-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/resume-azurermanalysisservicesserver)|Reanuda una instancia de servidor.|  
|[Set-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/set-azurermanalysisservicesserver)|Modifica una instancia de servidor.|   
|[Test-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/test-azurermanalysisservicesserver)|Existencia de Hola de pruebas de una instancia del servidor.| 

## <a name="database-operations"></a>Operaciones de la base de datos

Azure usan operaciones de base de datos de Analysis Services Hola mismo [SqlServer](https://www.powershellgallery.com/packages/SqlServer) módulo como SQL Server Analysis Services. Pero no todos los cmdlets son compatibles con Azure Analysis Services. 

módulo de SqlServer Hola proporciona cmdlets de administración de base de datos específica de la tarea como así como el cmdlet Invoke-ASCmd de propósito general de Hola que acepta un Tabular Model Scripting Language (TMSL) consultar o script. Hola se admiten siguientes cmdlets en el módulo SqlServer de Hola para Azure Analysis Services.

  
|Cmdlet|Descripción|
|------------|-----------------| 
|[Add-RoleMember](https://msdn.microsoft.com/library/hh510167.aspx)|Agregar un rol de base de datos de miembro tooa.| 
|[Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet)|Realiza una copia de seguridad de una base de datos de Analysis Services.|  
|[Remove-RoleMember](https://msdn.microsoft.com/library/hh510173.aspx)|Quita un miembro de un rol de base de datos.|   
|[Invoke-ASCmd](https://msdn.microsoft.com/library/hh479579.aspx)|Ejecuta un script de TMSL.|
|[Invoke-ProcessASDatabase](https://msdn.microsoft.com/library/mt651773.aspx)|Procesa una base de datos.|  
|[Invoke-ProcessPartition](https://msdn.microsoft.com/library/hh510164.aspx)|Procesa una partición.| 
|[Invoke-ProcessTable](https://msdn.microsoft.com/library/mt651774.aspx)|Procesa una tabla.|  
|[Merge-Partition](https://msdn.microsoft.com/library/hh479576.aspx)|Combina una partición.|  
|[Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet)|Restaura una base de datos de Analysis Services.| 
  

## <a name="related-information"></a>Información relacionada

* [Descarga del módulo de PowerShell de SQL Server](https://docs.microsoft.com/sql/ssms/download-sql-server-ps-module)   
* [Descarga de SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)   
* [Módulo de SqlServer en Galería de PowerShell](https://www.powershellgallery.com/packages/SqlServer)    
* [Programación de modelo tabular para el nivel de compatibilidad 1200 y superior](https://msdn.microsoft.com/library/mt712541.aspx)
