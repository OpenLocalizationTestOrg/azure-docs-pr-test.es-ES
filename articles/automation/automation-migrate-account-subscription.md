---
title: "aaaMigrate cuenta de automatización y los recursos | Documentos de Microsoft"
description: "Este artículo describe cómo toomove una automatización de la cuenta en automatización de Azure y recursos asociados de tooanother de una suscripción."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9c2db4a2-f324-48dc-8ce7-3343bf7230d5
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte
ms.openlocfilehash: 201c9091cd2d78d7ea407c1e5fb27f366bb4fa8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-automation-account-and-resources"></a>Migrar una cuenta de Automatización y sus recursos
Para las cuentas de automatización y los recursos asociados (es decir, activos, runbooks, módulos, etc.) que ha creado en hello portal de Azure y desea toomigrate desde un recurso de grupo tooanother o de tooanother de una suscripción, puede hacerlo fácilmente con Hola [mover recursos](../azure-resource-manager/resource-group-move-resources.md) característica disponible en hello portal de Azure. Sin embargo, antes de continuar con esta acción, primero debe revisar siguiente hello [lista de comprobación antes de mover recursos](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) y además, la lista de hello debajo tooAutomation específico.   

1. grupo de recursos/suscripción de destino de Hello debe estar en la misma región como origen de Hola.  Es decir, no se pueden mover cuentas de Automatización de una región a otra.
2. Al mover los recursos (por ejemplo, runbooks, trabajos, etc.), los grupos de código fuente de Hola y Hola destino se bloquean durante Hola de operación de Hola. Escribir y eliminar operaciones están bloqueados en grupos de hello hasta que se completa el movimiento de Hola.  
3. Los runbooks o las variables que hacen referencia a un identificador de recursos o suscripción de la suscripción existente Hola deberá toobe actualiza una vez completada la migración.   

> [!NOTE]
> Con esta característica no se pueden mover recursos de Automatización clásicos.
>
>

## <a name="toomove-hello-automation-account-using-hello-portal"></a>Cuenta de automatización mediante el portal de Hola Hola a toomove
1. En su cuenta de automatización, haga clic en **mover** princip Hola de hoja de Hola.<br> ![Opción Mover](media/automation-migrate-account-subscription/automation-menu-move.png)<br>
2. En hello **mover recursos** hoja, tenga en cuenta que presenta tooboth de recursos relacionados con su cuenta de automatización y los grupos de recursos.  Seleccione hello **suscripción** y **grupo de recursos** de listas desplegables de Hola u Hola seleccione opción **crear un nuevo grupo de recursos** y escriba un nuevo nombre de grupo de recursos en campo de Hello proporcionado.  
3. Revise y seleccione Hola casilla tooacknowledge se *comprender will scripts y herramientas necesidad toobe actualiza toouse nuevos identificadores de recursos después de que se han movido recursos* y, a continuación, haga clic en **Aceptar**.<br> ![Hoja Mover recursos](media/automation-migrate-account-subscription/automation-move-resources-blade.png)<br>   

Esta acción tendrá varias toocomplete minutos.  En **Notificaciones**, aparecerá el estado de cada acción que haya tenido lugar: validación, migración y, por último, cuando el proceso finalice.     

## <a name="toomove-hello-automation-account-using-powershell"></a>toomove Hola cuenta de automatización mediante PowerShell
toomove existente suscripción, utilice Hola o grupo de recursos de automatización recursos tooanother **Get-AzureRmResource** cuenta de automatización específico de cmdlet tooget hello y, a continuación, **Move-AzureRmResource** Mueva el cmdlet tooperform Hola.

Hola primer ejemplo muestra cómo toomove una automatización cuenta tooa nuevo grupo de recursos.

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

Después de ejecutar Hola ejemplo de código anterior, es posible que tooverify solicitada desea tooperform esta acción.  Una vez que pulses **Sí** y permitirá Hola tooproceed de script, no recibirá ninguna notificación mientras está realizando la migración de Hola.  

toomove tooa nueva suscripción, especifique un valor para hello *DestinationSubscriptionId* parámetro.

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

Al igual que con el ejemplo anterior de hello, será tooconfirm solicitadas Hola move.  

## <a name="next-steps"></a>Pasos siguientes
* Para obtener más información acerca de cómo mover grupo de recursos de toonew de recursos o suscripción, vea [Mover grupo de recursos de toonew de recursos o suscripción](../azure-resource-manager/resource-group-move-resources.md)
* Para obtener más información sobre el Control de acceso basado en roles en automatización de Azure, consulte demasiado[control de acceso basado en roles en automatización de Azure](automation-role-based-access-control.md).
* toolearn acerca de los cmdlets de PowerShell para administrar su suscripción, vea [mediante PowerShell de Azure con el Administrador de recursos](../azure-resource-manager/powershell-azure-resource-manager.md)
* toolearn acerca de características del portal para administrar su suscripción, vea [uso de recursos de hello Azure Portal toomanage](../azure-resource-manager/resource-group-portal.md).
