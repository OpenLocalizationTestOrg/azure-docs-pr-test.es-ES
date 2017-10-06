---
title: vista de grupo de aaaIntroduction toosecurity en Monitor de red de Azure | Documentos de Microsoft
description: "Esta página proporciona una visión general de hello capacidad de vista de seguridad de Monitor de red"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: ad27ab85-9d84-4759-b2b9-e861ef8ea8d8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: c2f6dbbffd0aedbb9db4b69d1758f2e66dd7abb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonetwork-security-group-view-in-azure-network-watcher"></a>Vista de grupo de seguridad de introducción toonetwork en Monitor de red de Azure

Los grupos de seguridad de red pueden asociarse a un nivel de subred o a un nivel de NIC. Cuando se asocia a un nivel de subred, se aplican a instancias de máquina virtual de tooall hello en la subred de Hola. Vista de grupo de seguridad de red devuelve todas las reglas que están asociadas en un nivel de formación y la subred para una máquina virtual que proporciona una visión general de configuración de Hola y Hola configurado NSG. Además, las reglas de seguridad eficaz Hola se devuelven para cada una de las NICs hello en una máquina virtual. Con la vista de grupos de seguridad de red, se puede evaluar una máquina virtual en busca de vulnerabilidades de red, como puertos abiertos. También puede validar si el grupo de seguridad de red está funcionando según lo previsto en función de un [configurado de comparación entre Hola y Hola reglas de seguridad eficaz](network-watcher-nsg-auditing-powershell.md).

Un caso de uso más extendido se encuentra en el cumplimiento de seguridad y auditoría. Puede definir un conjunto prescriptivo de reglas de seguridad como modelo para la regulación de la seguridad de su organización. Una auditoría periódica del cumplimiento puede implementarse en un mecanismo de programación mediante la comparación de reglas preceptivas de hello con reglas de hello efectivo para cada una de las máquinas virtuales de hello en la red.

Hola reglas portales se dividen por efectivo, subred, interfaz de red y de forma predeterminada. Esto proporciona una vista sencilla en máquina virtual de hello las reglas aplicadas tooa. Un botón de descarga es siempre tooeasily descargar todas las reglas de seguridad de hello con independencia de la pestaña de hello en un archivo CSV.

![vista de grupos de seguridad][1]

Se pueden seleccionar reglas y se abre una nueva hoja prefijos de grupo de seguridad de red de origen y de destino de hello tooshow. En esta hoja puede navegar directamente toohello recurso de grupo de seguridad de red.

![obtención de detalles][2]

### <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo tooaudit la seguridad de red de grupo Configuración visitando [configuración del grupo de seguridad de red de auditoría con PowerShell](network-watcher-nsg-auditing-powershell.md)

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









