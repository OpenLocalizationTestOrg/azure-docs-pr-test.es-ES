---
title: "equilibrador de carga de aaaCreate una conexión a Internet: portal de Azure clásico | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un equilibrador de carga con conexión a Internet en el modelo de implementación clásica utilizando Hola portal de Azure clásico"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fa3e93c0-968a-472d-a17c-65665c050db2
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 27b0d5af6e7b493fa94a9dfbfa260483ae95a2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-classic-portal"></a>Empezar a crear un equilibrador de carga (clásica) en el portal de Azure clásico Hola de Internet

> [!div class="op_single_selector"]
> * [Portal de Azure clásico](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [CLI de Azure](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Servicios en la nube de Azure](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Antes de trabajar con recursos de Azure, es importante toounderstand que Azure tiene dos modelos de implementación: Administrador de recursos de Azure y clásico. Asegúrese de que comprende los [modelos de implementación y las herramientas](../azure-classic-rm.md) antes de trabajar con recursos de Azure. Puede ver documentación de Hola de distintas herramientas, haga clic en las pestañas de hello en parte superior de Hola de este artículo. Este artículo trata el modelo de implementación clásica de Hola. También puede [Obtenga información acerca de cómo toocreate una conexión a Internet cargar equilibrador mediante Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a>Configuración de un equilibrador de carga accesible desde Internet para máquinas virtuales

Tráfico de red de orden tooload saldo de hello Internet todas las máquinas virtuales de Hola de un servicio de nube, debe crear un conjunto con equilibrio de carga. Este procedimiento se supone que ya ha creado máquinas virtuales de Hola y que están todas en hello mismo servicio en la nube.

**tooconfigure un conjunto con equilibrio de carga para las máquinas virtuales**

1. Hola portal de Azure clásico, haga clic en **máquinas virtuales**y, a continuación, haga clic en nombre de Hola de una máquina virtual en el conjunto de equilibrio de carga de Hola.
2. Haga clic en **Puntos de conexión** y luego en **Agregar**.
3. En hello **agregar una máquina virtual de tooa de punto de conexión** página, haga clic en la flecha derecha Hola.
4. En hello **especificar detalles de Hola de punto de conexión de hello** página:

   * En **nombre**, escriba un nombre para el punto de conexión de Hola o seleccione el nombre de hello en lista de Hola de extremos predefinidos para protocolos comunes.
   * En **protocolo**, seleccione Protocolo de hello requeridos por tipo hello del extremo, TCP o UDP, según sea necesario.
   * En **puerto público y puerto privado**, escriba los números de puerto de Hola que desee Hola toouse de máquina virtual, según sea necesario. Puede usar el puerto privado de Hola y reglas de firewall en tráfico de tooredirect Hola máquinas virtuales de una manera que sea adecuada para su aplicación. puerto privado Hola puede ser Hola igual que el puerto público de Hola. Por ejemplo, para un extremo para el tráfico web (HTTP), podría asignar puerto 80 tooboth Hola públicas y privadas port.

5. Seleccione **crear un conjunto con equilibrio de carga**y, a continuación, haga clic en la flecha derecha Hola.
6. En hello **configurar el conjunto de equilibrio de carga de hello** página, escriba un nombre para el conjunto de equilibrio de carga de hello y, a continuación, asignar valores de hello para sondear el comportamiento de hello equilibrador de carga de Azure. Hola equilibrador de carga utiliza sondeos toodetermine si hay máquinas virtuales de hello en el conjunto de equilibrio de carga de hello tooreceive disponible el tráfico entrante.
7. Haga clic en el extremo de carga equilibrada de hello marca de verificación toocreate Hola. Verá **Sí** en hello **nombre de conjunto de carga equilibrada** columna de hello **extremos** página para la máquina virtual de Hola.
8. En el portal de hello, haga clic en **máquinas virtuales**, haga clic en nombre de Hola de una máquina virtual adicional en el conjunto de equilibrio de carga de hello, haga clic en **extremos**y, a continuación, haga clic en **agregar**.
9. En hello **agregar una máquina virtual en extremo tooa** página, haga clic en **Agregar conjunto de carga equilibrada existente de punto de conexión tooan**, seleccione Hola nombre de conjunto de equilibrio de carga de hello y, a continuación, haga clic en la flecha derecha de Hola.
10. En hello **especificar detalles de Hola de punto de conexión de hello** página, escriba un nombre para el extremo de hello y, a continuación, haga clic en la casilla de verificación Hola.

Para las máquinas virtuales adicionales de hello en el conjunto de equilibrio de carga de hello, repita los pasos 8-10.

## <a name="next-steps"></a>Pasos siguientes

[Introducción a la configuración de un equilibrador de carga interno](load-balancer-get-started-ilb-arm-ps.md)

[Configuración de un modo de distribución del equilibrador de carga](load-balancer-distribution-mode.md)

[Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga](load-balancer-tcp-idle-timeout.md)
