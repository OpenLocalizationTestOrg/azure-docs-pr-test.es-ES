---
title: "comprobar de tráfico de aaaVerify con flujo de IP de Monitor de red de Azure: portal de Azure | Documentos de Microsoft"
description: "Este artículo se describe cómo toocheck si se permite o deniega el tráfico tooor desde una máquina virtual"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e0e3e9a8-70eb-409a-a744-0ce9deb27148
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: abf639f36d32f3416dd927e66b635267b746e62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Compruebe si el tráfico se permitirá o denegará tooor de una máquina virtual con IP flujo comprobar un componente de Monitor de red de Azure

> [!div class="op_single_selector"]
> - [Portal de Azure](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [API de REST de Azure](network-watcher-check-ip-flow-verify-rest.md)


Flujo IP comprobar es una característica de Monitor de red que le permite tooverify si se permite el tráfico tooor desde una máquina virtual. validación de Hola se puede ejecutar para el tráfico entrante o saliente. Este escenario es útil tooget un estado actual del si una máquina virtual puede comunicarse un recurso externo tooan o algún otro recurso. Flujo IP comprobar puede ser usado tooverify si las reglas del grupo de seguridad de red (NSG) se han configurado correctamente y solucionar los problemas flujos que se bloquean las reglas de NSG. Otra razón para usar IP flujo Compruebe es que quiera bloquear el tráfico de tooensure está bloqueando correctamente hello NSG.

## <a name="before-you-begin"></a>Antes de empezar

Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red o tiene una instancia existente de Monitor de red. escenario de Hello también supone que un grupo de recursos con una máquina virtual válida existe toobe usa.

## <a name="scenario"></a>Escenario

Este escenario utiliza tooverify IP flujo comprobar si una máquina virtual puede comunicarse tooanother máquina a través del puerto 443. Si se deniega el tráfico de hello, devuelve la regla de seguridad de Hola que deniega ese tráfico. toolearn más información acerca de IP flujo comprobar, visite [Introducción comprobar flujo de IP](network-watcher-ip-flow-verify-overview.md)

### <a name="run-ip-flow-verify"></a>Ejecución de la Comprobación del flujo de IP

Navegue tooyour Monitor de red y haga clic en **comprobar flujo IP**. Seleccionar máquina virtual de Hola y la interfaz de red que desee tooverify tráfico desde. Escriba cualquier información adicional de filtrado y haga clic en **Comprobar**.

Una vez que pulses **comprobar**, se comprueba el flujo de hello en función de criterios de hello proporcionada. resultado de Hello sea **acceso permitido** o **acceso denegado**. Si se deniega el acceso, Hola grupo de seguridad de red (NSG) y se proporciona la regla de seguridad que bloquee el tráfico. Si la denegación de Hola de tráfico es el comportamiento esperado, regla de hello fue correcta.

> [!NOTE]
> Flujo IP comprobar requiere que se asigna el recurso de máquina virtual de Hola.

Como puede ver de hello después de la imagen, se permite el tráfico HTTPS saliente Hola.

![Información general sobre la comprobación del flujo de IP][1]

Tal como se muestra en hello después de la imagen, se cambia el tráfico hello y tooinbound too123 de cambiar el puerto de entrada. Ahora se deniega el tráfico, mensaje de bienvenida de "Acceso denegado" se proporciona junto con hello seguridad y el grupo de regla de seguridad que deniegan el tráfico de Hola.

![resultados de flujo de ip][2]

## <a name="next-steps"></a>Pasos siguientes

Si se está bloqueando el tráfico y no debe ser, consulte [administrar grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hacia abajo Hola red seguridad y el grupo de reglas de seguridad que se definen.

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













