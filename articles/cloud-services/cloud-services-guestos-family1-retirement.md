---
title: familia de SO aaaGuest 1 retirada Observe | Documentos de Microsoft
description: "Proporciona información acerca de cuándo se produjeron retirada Hola familia 1 del SO de invitado de Azure y cómo toodetermine si se ve afectado"
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 37b422e9-0713-4a81-a942-f553ef478064
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/21/2017
ms.author: raiye
ms.openlocfilehash: fa8b904c6560dbbe4982c301f818c7a5cbc4eacb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="guest-os-family-1-retirement-notice"></a>Aviso de retirada de la familia 1 del SO invitado
retirada de Hola de familia 1 del SO se presentó por primera vez en el 1 de junio de 2013.

**2 de septiembre de 2014** hello Azure sistema operativo (SO invitado) familia 1.x, que se basa en el sistema operativo de Windows Server 2008 hello, se retira oficialmente. Todos los intentos de toodeploy nuevos servicios o actualizar servicios existentes con la familia 1 se producirá un error con un mensaje de error que informa que Hola que se ha retirado la familia 1 del SO invitado.

**3 de noviembre de 2014** El soporte extendido para la familia 1 del SO invitado finaliza y se retira completamente. Todos los servicios todavía en la familia 1 se verá afectados. Podemos detener dichos servicios en cualquier momento. No hay ninguna garantía de que los servicios continúen toorun a menos que los actualice manualmente.

Si tiene preguntas adicionales, visite hello [foros de servicios de nube](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) o [póngase en contacto con soporte técnico de Azure](https://azure.microsoft.com/support/options/).

## <a name="are-you-affected"></a>Cómo saber si se ve afectado
Servicios en la nube se ven afectados si se aplica cualquiera de hello siguientes:

1. Tiene un valor de "osFamily ="1"especifica explícitamente en el archivo ServiceConfiguration.cscfg de hello para el servicio de nube.
2. No tiene un valor para osFamily especifica explícitamente en el archivo ServiceConfiguration.cscfg de hello para el servicio de nube. Actualmente, sistema de Hola usa Hola predeterminado valor de "1" en este caso.
3. Hola portal de Azure indica el valor de familia de sistema operativo invitado como "Windows Server 2008".

toofind qué de servicios en la nube qué familia del SO se están ejecutando, puede ejecutar Hola siguiente secuencia de comandos de PowerShell de Azure, aunque primero debe [configurar Azure PowerShell](/powershell/azureps-cmdlets-docs) primero. Para obtener más información sobre el script de Hola, consulte [Azure invitado SO familia 1 final del ciclo de vida: junio de 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

Servicios en la nube se verá afectados por la familia 1 del SO retirada si la columna de osFamily hello en la salida del script de Hola está vacío o contiene un "1".

## <a name="recommendations-if-you-are-affected"></a>Recomendaciones en caso de verse afectado
Se recomienda que migre su tooone de roles de servicio en la nube de familias del SO invitado Hola admitida:

**Familia 4.x del SO invitado** : Windows Server 2012 R2 *(recomendado)*

1. Asegúrese de que la aplicación use el SDK 2.1 o posterior con .NET Framework 4.0, 4.5 o 4.5.1.
2. Establecer archivo ServiceConfiguration.cscfg de hello osFamily atributo hello en demasiado "4" y volver a implementar su servicio en la nube.

**Familia 3.x del SO invitado** : Windows Server 2012

1. Asegúrese de que la aplicación use el SDK 1.8 o posterior con .NET Framework 4.0 o 4.5.
2. Establecer archivo ServiceConfiguration.cscfg de hello osFamily atributo hello en demasiado "3" y volver a implementar su servicio en la nube.

**Familia 2.x del SO invitado** : Windows Server 2008 R2

1. Asegúrese de que la aplicación use el SDK 1.3 o posterior con .NET Framework 3.5 o 4.0.
2. Establecer archivo ServiceConfiguration.cscfg de hello osFamily atributo hello en demasiado "2" y vuelva a implementar el servicio de nube.

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a>El soporte extendido para la familia 1 del SO invitado finalizó el 3 de noviembre de 2014.
Los servicios en la nube de la familia 1 del SO invitado ya no son compatibles. Migre la familia 1 tan pronto como tooavoid posibles interrupciones de servicio.  

## <a name="next-steps"></a>Pasos siguientes
Hola de revisión más reciente [versiones del SO invitado](cloud-services-guestos-update-matrix.md).
