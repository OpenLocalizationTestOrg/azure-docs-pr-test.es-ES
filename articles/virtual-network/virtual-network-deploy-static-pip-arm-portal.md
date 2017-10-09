---
title: "aaaCreate una máquina virtual con una dirección pública estática de IP - portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una máquina virtual con una estática pública IP dirección utilizando Hola portal de Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e9546bcc-f300-428f-b94a-056c5bd29035
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f74d2132785f06148757409ee0a44b98d1e4b98e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-portal"></a>Crear una máquina virtual con una dirección IP pública estática con hello portal de Azure

> [!div class="op_single_selector"]
> * [Portal de Azure](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [CLI de Azure](virtual-network-deploy-static-pip-arm-cli.md)
> * [Plantilla](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (clásico)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md). Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar del modelo de implementación clásica de Hola.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a>Creación de una máquina virtual con una IP pública estática

toocreate una máquina virtual con una dirección IP pública estática de las direcciones de hello portal de Azure, Hola completa pasos:

1. Desde un explorador, navegue toohello [portal de Azure](https://portal.azure.com) y, si es necesario, inicie sesión con su cuenta de Azure.
2. En la esquina superior izquierda de hello del portal de hello, haga clic en **New**>>**proceso**>**Windows Server 2012 R2 Datacenter**.
3. Hola **seleccionar un modelo de implementación** seleccione **el Administrador de recursos** y haga clic en **crear**.
4. Hola **Fundamentos** hoja, escriba la información de la máquina virtual de hello tal y como se muestra a continuación y, a continuación, haga clic en **Aceptar**.
   
    ![Portal de Azure: conceptos básicos](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. Hola **elegir un tamaño de** hoja, haga clic en **estándar A1** tal y como se muestra a continuación y, a continuación, haga clic en **seleccione**.
   
    ![Portal de Azure: elegir un tamaño](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. Hola **configuración** hoja, haga clic en **dirección IP pública**, a continuación, en hello **Crear dirección IP pública** hoja, en **asignación**, haga clic en **Estático** tal y como se muestra a continuación. A continuación, haga clic en **Aceptar**.
   
    ![Portal de Azure: crear la dirección IP pública](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. Hola **configuración** hoja, haga clic en **Aceptar**.
8. Hola de revisión **resumen** hoja, tal y como se muestra a continuación y, a continuación, haga clic en **Aceptar**.
   
    ![Portal de Azure: crear la dirección IP pública](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. Observe el nuevo icono de hello en el panel.
   
    ![Portal de Azure: crear la dirección IP pública](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. Una vez que se crea Hola VM, Hola **configuración** hoja se mostrarán tal y como se muestra a continuación
    
    ![Portal de Azure: crear la dirección IP pública](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

