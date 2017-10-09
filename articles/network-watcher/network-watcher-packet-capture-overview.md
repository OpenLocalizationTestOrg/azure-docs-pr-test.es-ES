---
title: captura de tooPacket aaaIntroduction en Monitor de red de Azure | Documentos de Microsoft
description: "Esta página proporciona una visión general de la capacidad de captura de paquetes de saludo Monitor de red"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3a81afaa-ecd9-4004-b68e-69ab56913356
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2ce01b391b9c1a1c19aa29c8620628c55586df03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toovariable-packet-capture-in-azure-network-watcher"></a>Captura de paquetes toovariable de introducción en el Monitor de red de Azure

Captura de paquetes de variable de Monitor de red le permite toocreate paquete captura sesiones tootrack tráfico tooand desde una máquina virtual. Captura de paquetes le ayuda a anomalías red toodiagnose reactivamente y proactivity. Otros usos incluyen la recopilación de estadísticas de red, obtenga información sobre las intrusiones de red, toodebug cliente-servidor las comunicaciones y mucho más.

La captura de paquetes es una extensión de máquina virtual que se inicia de forma remota a través de Network Watcher. Esta capacidad facilita la carga de Hola de ejecutar manualmente una captura de paquetes en la máquina virtual de hello deseado, que permite ahorrar tiempo. Captura de paquetes puede realizarse a través del portal de hello, PowerShell, CLI o API de REST. Un ejemplo de cómo se puede activar la captura de paquetes es con las alertas de la máquina virtual. Los filtros son proporcionados para tooensure de sesión de captura de Hola captura el tráfico que desee toomonitor. Los filtros se basan en la información de 5-tupla (protocolo, dirección IP local, dirección IP remota, el puerto local y puerto remoto). Hola capturan datos se almacenan en el disco local de Hola o un blob de almacenamiento. Hay un límite de 10 sesiones de captura de paquetes por región y suscripción. Este límite aplica solo a las sesiones de toohello y no hay ningún toohello archivos de captura de paquetes de guardados localmente en hello VM o en una cuenta de almacenamiento.

> [!IMPORTANT]
> La captura de paquetes requiere una extensión de máquina virtual `AzureNetworkWatcherExtension`. Para instalar la extensión de hello en una máquina virtual de Windows, visite [extensión de máquina virtual de agente de Monitor de red de Azure para Windows](../virtual-machines/windows/extensions-nwa.md) y para la visita de VM de Linux [extensión de máquina virtual de agente de Monitor de red de Azure para Linux](../virtual-machines/linux/extensions-nwa.md).

información de hello tooreduce capturar información de hello tooonly que desee, Hola siguientes opciones está disponible para una sesión de captura de paquetes:

**Configuración de captura**

|Propiedad|Descripción|
|---|---|
|**Número máximo de bytes por paquete (bytes)** | Hola número de bytes de cada paquete que se capturan, se capturan todos los bytes si se deja en blanco. Hola número de bytes de cada paquete que se capturan, se capturan todos los bytes si se deja en blanco. Si tiene un solo encabezado de IPv4 de hello: indicar 34 aquí |
|**Número máximo de bytes por sesión (bytes)** | Número total de bytes en la se captura, una vez que se alcanza el valor de Hola Hola finaliza la sesión.|
|**Límite de tiempo (segundos)** | Establece una restricción horaria en el paquete de saludo capturar sesión. valor predeterminado de Hello es 18000 segundos o 5 horas.|

**Filtrado (opcional)**

|Propiedad|Descripción|
|---|---|
|**Protocolo** | captura de Hello toofilter de protocolo para el paquete de saludo. los valores disponibles de Hello son TCP, UDP y todos.|
|**Dirección IP local** | Este valor filtra toopackets de captura de paquetes de saludo donde la dirección IP local Hola coincide con este valor de filtro.|
|**Puerto local** | Este paquete de saludo de filtros de valor capturar toopackets donde puerto local Hola coincide con este valor de filtro.|
|**Dirección IP remota** | Este paquete de saludo de filtros de valor capturar toopackets donde hello remoto IP coincide con este valor de filtro.|
|**Puerto remoto** | Este paquete de saludo de filtros de valor capturar toopackets donde puerto remoto hello coincide con este valor de filtro.|

### <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo administrar las capturas de paquetes a través del portal de hello visitando [administrar captura de paquetes en el portal de Azure hello](network-watcher-packet-capture-manage-portal.md) o con PowerShell visitando [administrar paquetes de captura con PowerShell](network-watcher-packet-capture-manage-powershell.md).

Obtenga información acerca de cómo se captura toocreate automático paquetes basados en alertas de máquina virtual visitando [crear una captura de paquetes desencadenadas alerta](network-watcher-alert-triggered-packet-capture.md)

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













