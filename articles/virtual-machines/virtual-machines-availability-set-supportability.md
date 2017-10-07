---
title: "aaaSupportability de Agregar conjunto de disponibilidad existente de máquinas virtuales de Azure tooan | Documentos de Microsoft"
description: "Compatibilidad de Agregar conjunto de disponibilidad de máquinas virtuales de Azure tooan existente."
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/15/2017
ms.author: delhan
ms.openlocfilehash: dc2bd86b916f1d1a0a0d4c9e870df829434c96b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="supportability-of-adding-azure-vms-tooan-existing-availability-set"></a>Compatibilidad de Agregar conjunto de disponibilidad de máquinas virtuales de Azure tooan existente

En ocasiones, puede encontrar limitaciones cuando se agrega nuevas máquinas virtuales (VM) tooan conjunto de disponibilidad existente. Hola Hola a las series VM se pueden mezclar en el mismo conjunto de disponibilidad de detalles de gráfico siguientes.

Aquí es Hola compatibilidad toomix diferentes tipos de matriz de máquinas virtuales:

Serie y conjunto de disponibilidad|Segunda máquina virtual|Una |Av2|D|Dv2|Dv3|
|---|---|---|---|---|---|---|
|Primera máquina virtual|||||||
|Una ||OK|OK|OK|OK|OK|
|Av2||OK|OK|OK|OK|OK|
|D||OK|OK|OK|OK|OK|
|Dv2||OK|OK|OK|OK|OK|
|Dv3||OK|OK|OK|OK|OK|

No se pudo todas las otras series de hello conjunto de disponibilidad mismo porque requieren un hardware específico.
