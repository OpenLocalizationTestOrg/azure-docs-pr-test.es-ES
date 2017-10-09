---
title: "servicios en la nube aaaOptions para la depuración de Azure | Documentos de Microsoft"
description: "Depuración de servicios en la nube de Azure"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 80755da7-8350-4f5c-97ce-2962beabb36d
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/18/2017
ms.author: kraigb
ms.openlocfilehash: 8b7779ca33cfd82fd5fbccf229ea822c311bdea0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="learn-hello-various-ways-toodebug-an-azure-cloud-service"></a>Obtenga información acerca de diversas maneras de hello toodebug un servicio de nube de Azure
Este artículo proporciona vínculos toohello varias formas toodebug un servicio de nube de Azure. 

## <a name="debugging-an-azure-cloud-service-in-visual-studio"></a>Depuración de un servicio en la nube de Azure en Visual Studio
Se puede ahorrar tiempo y dinero utilizando hello Azure compute emulator toodebug su servicio en la nube en un equipo local. La depuración de un servicio localmente antes de su implementación puede mejorar la fiabilidad y el rendimiento sin pagar por tiempo de proceso. No obstante, podrían producirse algunos errores solo al ejecutar un servicio en la nube en Azure. Al habilitar la depuración remota al publicar su servicio y, a continuación, asociar instancia de rol de hello depurador tooa, se pueden depurar errores que se producen sólo cuando se ejecuta un servicio de nube en Azure. Para obtener más información, consulte [Depuración del servicio en la nube en el equipo local](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-your-cloud-service-on-your-local-computer).

## <a name="using-azure-diagnostics"></a>Uso de Azure Diagnostics 
Puede utilizar el diagnóstico de Azure toolog obtener información de ejecución de código en roles, si se están ejecutando los roles de hello en el entorno de desarrollo de Hola o en Azure. Para más información, consulte [Habilitación de diagnósticos de Azure en servicios en la nube de Azure](http://go.microsoft.com/fwlink/p/?LinkId=400450).

## <a name="using-intellitrace"></a>Uso de IntelliTrace 
Si usa funciones de Visual Studio Enterprise toowrite como destino .NET Framework 4.5, puede habilitar IntelliTrace en vez de Hola que implementa un servicio de nube de Azure desde Visual Studio. IntelliTrace proporciona un registro que se puede usar con Visual Studio toodebug la aplicación como si se estuviera ejecutando en Azure. Para obtener más información, vea [Depurar con IntelliTrace y Visual Studio un servicio en la nube](http://go.microsoft.com/fwlink/p/?LinkId=623016).

## <a name="remote-debugging"></a>Depuración remota 
Puede habilitar la depuración remota en los servicios de nube en tiempo de hello cuando se implementa un servicio nube Hola desde Visual Studio. Si elige tooenable para una implementación de la depuración remota, servicios de depuración remota se instalan en máquinas virtuales de Hola que se ejecutan cada instancia de rol. Estos servicios, como `msvsmon.exe`, no afectan al rendimiento ni al resultado en cuanto a costos adicionales. Para obtener más información, consulte [Depuración de un servicio en la nube en Azure](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-a-cloud-service-in-azure).

## <a name="next-steps"></a>Pasos siguientes
- [Depurar un servicio de nube de Azure o una máquina virtual en Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md) -obtener información detallada de Hola de cómo toodebug Azure servicios en la nube.
