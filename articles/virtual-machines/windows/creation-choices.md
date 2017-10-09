---
title: aaaDifferent formas toocreate una VM de Windows en Azure | Documentos de Microsoft
description: "Muestra diferentes maneras de hello toocreate una máquina virtual de Windows con el Administrador de recursos."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 809ba8f4-b54e-43c5-bbe3-8e710c49971f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2928d4daa9b44c4d3a5083092a82c9a7f7c69fae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-windows-virtual-machine"></a>Diferentes maneras toocreate una máquina virtual Windows

Azure ofrece toocreate de distintas formas una máquina virtual porque las máquinas virtuales son adecuadas para fines y los distintos usuarios. Esto significa que necesita toomake algunas decisiones sobre la máquina virtual de Hola y cómo toocreate lo. Este artículo proporciona un resumen de estas opciones y vincula tooinstructions.

## <a name="azure-portal"></a>Azure Portal
El uso de hello portal de Azure es un tootry de manera sencilla a una máquina virtual, sobre todo si se está empezando con Azure. 

[Crear una máquina virtual con Windows y portal de Hola](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a>Plantilla
Las máquinas virtuales requieren una combinación de recursos (por ejemplo, conjuntos de disponibilidad y cuentas de almacenamiento). En lugar de implementar y administrar cada recurso por separado, puede crear una plantilla de Azure Resource Manager que implementa y aprovisiona todos los recursos de hello en una única operación coordinada.

* [Creación de una máquina virtual Windows con una plantilla del Administrador de recursos](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a>Azure PowerShell
Si prefiere trabajar en un shell de comandos, puede usar PowerShell de Azure.

* [Creación de una máquina virtual Windows con PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a>Visual Studio
Usar Visual Studio toobuild, administrar e implementar las máquinas virtuales con hello Azure Tools para Visual Studio y Hola SDK de Azure.

[Herramientas de Azure para Visual Studio](https://www.visualstudio.com/features/azure-tools-vs)

