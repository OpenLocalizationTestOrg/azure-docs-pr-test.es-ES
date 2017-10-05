---
title: Escalado de un servicio en la nube de Azure en Windows PowerShell | Microsoft Docs
description: "(modelo clásico) Aprenda a usar PowerShell para escalar o reducir horizontalmente un rol web o de trabajo en Azure."
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: ee37dd8c-6714-4c61-adb8-03d6bbf76c9a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: mmccrory
ms.openlocfilehash: a7ae8ff202d403dff19b8c9a6a09492235db27ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-scale-a-cloud-service-in-powershell"></a>Escalado de un servicio en la nube en PowerShell

Puede usar Windows PowerShell para escalar o reducir horizontalmente un rol web o de trabajo mediante la adición o eliminación de instancias.  

## <a name="log-in-to-azure"></a>Inicie sesión en Azure.

Para poder realizar cualquier operación en su suscripción a través de PowerShell, debe iniciar sesión:

```powershell
Add-AzureAccount
```

Si tiene varias suscripciones asociadas a su cuenta, puede que deba cambiar la suscripción actual (según donde resida el servicio en la nube). Para comprobar la suscripción actual, ejecute:

```powershell
Get-AzureSubscription -Current
```

Si necesita cambiar la suscripción actual, ejecute:

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-the-current-instance-count-for-your-role"></a>Comprobación del número actual de instancias para el rol

Para comprobar el estado actual de su rol, ejecute:

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

Obtendrá información sobre el rol, como su versión actual de SO y el número de instancias. En este caso, el rol tiene una sola instancia.

![Información sobre el rol](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-the-role-by-adding-more-instances"></a>Escalado horizontal del rol mediante la adición de más instancias

Para escalar horizontalmente su rol, pase el número deseado de instancias como el parámetro **Count** al cmdlet **Set-AzureRole**:

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

El cmdlet se bloquea momentáneamente mientras las nuevas instancias se aprovisionan e inician. Durante este tiempo, si abre una nueva ventana de PowerShell y llama a **Get-AzureRole** como se mostró anteriormente, verá el nuevo recuento de instancias de destino. Y si examina el estado del rol en el portal, verá que se inicia la nueva instancia:

![Instancia de máquina virtual iniciándose en el portal](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

Cuando se hayan iniciado las nuevas instancias, el cmdlet devolverá resultados correctamente:

![Éxito del aumento de instancias de rol](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-the-role-by-removing-instances"></a>Reducción horizontal del rol mediante la eliminación de instancias

Puede reducir un rol horizontalmente quitando instancias de la misma manera. Establezca el parámetro **Count** de **Set-AzureRole** en el número de instancias que quiere tener después de que finalice la operación de reducción horizontal.

## <a name="next-steps"></a>Pasos siguientes

No es posible configurar el escalado automático para los servicios en la nube de PowerShell. Para ello, consulte [Cómo escalar automáticamente un servicio en la nube](cloud-services-how-to-scale-portal.md).
