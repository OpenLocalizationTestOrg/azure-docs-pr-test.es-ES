---
title: "tráfico de aaaVerify con Azure red Monitor IP flujo comprobar - CLI de Azure | Documentos de Microsoft"
description: "Este artículo se describe cómo toocheck si tooor de tráfico de una máquina virtual se permite o deniega con CLI de Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c6becc5c142837b04d15490b2b3bd11124434570
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


Flujo de IP comprobar es una característica de Monitor de red que le permite tooverify si se permite el tráfico tooor desde una máquina virtual. Este escenario es útil tooget un estado actual del si una máquina virtual puede comunicarse un recurso externo tooan o back-end. Flujo IP comprobar puede ser usado tooverify si las reglas del grupo de seguridad de red (NSG) se han configurado correctamente y solucionar los problemas flujos que se bloquean las reglas de NSG. Otra razón para usar IP flujo Compruebe es que quiera bloquear el tráfico de tooensure está bloqueando correctamente hello NSG.

En este artículo, se utiliza la multiplataforma Azure CLI 1.0, que está disponible para Windows, Mac y Linux.

## <a name="before-you-begin"></a>Antes de empezar

Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red o tiene una instancia existente de Monitor de red. escenario de Hello también supone que un grupo de recursos con una máquina virtual válida existe toobe usa.

## <a name="scenario"></a>Escenario

Este escenario usa tooverify IP flujo comprobar si una máquina virtual puede comunicarse conocidos tooa dirección IP de Bing. Si se deniega el tráfico de hello, devuelve la regla de seguridad de Hola que deniega ese tráfico. toolearn más información acerca de IP flujo comprobar, visite [Introducción comprobar flujo de IP](network-watcher-ip-flow-verify-overview.md)


## <a name="get-a-vm"></a>Obtención de una máquina virtual

Flujo IP Compruebe tooor de tráfico de pruebas desde una dirección IP en un tooor de máquina virtual de un destino remoto. Un identificador de una máquina virtual se requiere para hello cmdlet. Si ya conoce el identificador de Hola de hello toouse de máquina virtual, puede omitir este paso.

```
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="get-hello-nics"></a>Obtener Hola NIC

se necesita la dirección IP de Hola de una NIC en la máquina virtual de Hola, en este ejemplo recuperamos Hola NIC en una máquina virtual. Si ya sabe Hola IP de direcciones que desea tootest en la máquina virtual de hello, puede omitir este paso.

```
azure network nic show -g resourceGroupName -n nicName
```

## <a name="run-ip-flow-verify"></a>Ejecución de la Comprobación del flujo de IP

Ahora que tenemos información Hola necesarios toorun Hola cmdlet, ejecutamos hello `network watcher ip-flow-verify` tráfico de cmdlet tootest Hola. En este ejemplo, estamos utilizando dirección IP de la primera hello en la NIC de hello primero.

```
azure network watcher ip-flow-verify -g resourceGroupName -n networkWatcherName -t targetResourceId -d directionInboundorOutbound -p protocolTCPorUDP -o localPort -m remotePort -l localIpAddr -r remoteIpAddr
```

> [!NOTE]
> Flujo de IP comprobar requiere que el recurso de máquina virtual de Hola se asigna toorun.

## <a name="review-results"></a>Revisión de los resultados

Después de ejecutar `network watcher ip-flow-verify` Hola resultados se devuelven, en el ejemplo siguiente se hello es Hola devuelva resultados de hello anterior paso.

```
data:    Access                          : Deny
data:    Rule Name                       : defaultSecurityRules/DefaultInboundDenyAll
info:    network watcher ip-flow-verify command OK
```

## <a name="next-steps"></a>Pasos siguientes

Si se está bloqueando el tráfico y no debe ser, consulte [administrar grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hacia abajo Hola red seguridad y el grupo de reglas de seguridad que se definen.

Obtenga información acerca de tooaudit la configuración de NSG visitando [auditoría red seguridad grupos (NSG) con el Monitor de red](network-watcher-nsg-auditing-powershell.md).

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
