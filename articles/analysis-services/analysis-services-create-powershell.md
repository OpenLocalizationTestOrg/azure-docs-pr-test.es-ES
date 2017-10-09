---
title: aaaCreate un servidor de Analysis Services de Azure mediante PowerShell | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una Azure Analysis Services server usando PowerShell"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/01/2017
ms.author: owend
ms.custom: mvc
ms.openlocfilehash: 269b78983410f773d47c4cea34d6d353b19f9e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a>Creación de un servidor de Azure Analysis Services mediante PowerShell

Este tutorial rápido describe el uso de PowerShell de hello toocreate de línea de comandos un servidor de Analysis Services de Azure en un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md) en su suscripción de Azure.

Esta tarea requiere la versión 4.0 del módulo de Azure PowerShell, o cualquier versión posterior. versión de hello toofind, ejecute ` Get-Module -ListAvailable AzureRM`. tooinstall o actualización, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps). 

> [!NOTE]
> La creación de un servidor puede dar lugar a un nuevo servicio facturable. más información, consulte toolearn [precios de Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).

## <a name="prerequisites"></a>Requisitos previos
toocomplete este tutorial rápido, necesita:

* **Suscripción de Azure**: visite [evaluación gratuita de Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate una cuenta.
* **Azure Active Directory**: la suscripción debe estar asociada a un inquilino de Azure Active Directory y debe tener una cuenta en ese directorio. más información, consulte toolearn [permisos de usuario y la autenticación](analysis-services-manage-users.md).

## <a name="import-azurermanalysisservices-module"></a>Importación del módulo AzureRm.AnalysisServices
toocreate un servidor en su suscripción, usas hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) módulo del componente. Cargar el módulo de AzureRm.AnalysisServices de hello en la sesión de PowerShell.

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-tooazure"></a>Inicie sesión en tooAzure

Inicie sesión en tooyour suscripción de Azure mediante hello [AzureRmAccount agregar](/powershell/module/azurerm.profile/add-azurermaccount) comando. Siga hello en pantalla de instrucciones.

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a>Crear un grupo de recursos
 
Un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md) es un contenedor lógico en el que se implementan y se administran los recursos de Azure como grupo. Cuando cree el servidor, deberá especificar un grupo de recursos de su suscripción. Si no dispone de un grupo de recursos, puede crear uno nuevo mediante el uso de hello [AzureRmResourceGroup New](/powershell/module/azurerm.resources/new-azurermresourcegroup) comando. Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en la región del oeste de Estados Unidos de Hola.

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a>Creación de un servidor

Crear un nuevo servidor mediante el uso de hello [AzureRmAnalysisServicesServer New](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) comando. Hello siguiente ejemplo crea un servidor denominado myServer en myResourceGroup de región del oeste de EE. Hola, en el nivel de hello D1 y especifica philipc@adventureworks.com como un administrador del servidor.

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a>Limpieza de recursos

Puede quitar servidor hello de su suscripción mediante el uso de hello [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) comando. Si va a seguir con otros inicios rápidos y tutoriales de esta colección, no quite el servidor. Hello en el ejemplo siguiente se quita servidor hello creado en el paso anterior de Hola.


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a>Pasos siguientes
[Administración de Azure Analysis Services con PowerShell](analysis-services-powershell.md)   
[Implementación de un modelo desde SSDT](analysis-services-deploy.md)   
[Creación de un modelo en Azure Portal](analysis-services-create-model-portal.md)