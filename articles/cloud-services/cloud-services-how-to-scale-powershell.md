---
title: aaaScale un servicio de nube de Azure en Windows PowerShell | Documentos de Microsoft
description: "(clásico) Obtenga información acerca de cómo toouse PowerShell tooscale un rol web o el rol de trabajo o alejar en Azure."
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
ms.openlocfilehash: cfac6660e84f8ae24e4e9bdd5bf2016fb9cd7045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-a-cloud-service-in-powershell"></a>¿Cómo tooscale una nube de servicio en PowerShell

Puede usar Windows PowerShell tooscale un rol web o el rol de trabajo o agregando o quitando instancias.  

## <a name="log-in-tooazure"></a>Inicie sesión en tooAzure

Para poder realizar cualquier operación en su suscripción a través de PowerShell, debe iniciar sesión:

```powershell
Add-AzureAccount
```

Si tiene varias suscripciones asociadas a su cuenta, deberá suscripción actual de hello toochange según donde reside el servicio de nube. toocheck Hola suscripción actual, ejecute:

```powershell
Get-AzureSubscription -Current
```

Si necesita la suscripción actual de hello toochange, ejecute:

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-hello-current-instance-count-for-your-role"></a>Compruebe el número de instancias actual de hello para el rol

estado actual de hello toocheck de su rol, ejecute:

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

Obtendrá información sobre el rol de hello, incluidos su número de versión e instancia de SO actual. En este caso, el rol de hello tiene una sola instancia.

![Obtener información sobre el rol de Hola](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-hello-role-by-adding-more-instances"></a>Escalar horizontalmente el rol de hello mediante la adición de más instancias

tooscale horizontal de su rol, pase Hola número deseado de instancias como hello **recuento** parámetro toohello **Set-AzureRole** cmdlet:

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

bloques de cmdlet Hola momentáneamente al nuevas instancias de Hola se aprovisionan y se inicia. Durante este tiempo, si abre una nueva ventana de PowerShell y llamada **Get-AzureRole** tal y como se muestra anteriormente, verá recuento de instancias de destino nuevo Hola. Y si examina el estado del rol de hello en el portal de hello, debería ver instancia nueva de hello iniciar:

![Instancia de máquina virtual iniciándose en el portal](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

Una vez que se hayan iniciado las instancias nuevas de hello, Hola cmdlet devolverá correctamente:

![Éxito del aumento de instancias de rol](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-hello-role-by-removing-instances"></a>Escalar en función de hello mediante la eliminación de instancias

Puede escalar en un rol mediante la eliminación de instancias en hello igual. Conjunto hello **recuento** parámetro en **Set-AzureRole** toohello número de instancias que desee toohave una vez completada la escala de hello en la operación.

## <a name="next-steps"></a>Pasos siguientes

No es posible tooconfigure Autoescala para servicios en la nube de PowerShell. toodo que vea [cómo tooauto escalar un servicio de nube](cloud-services-how-to-scale-portal.md).
