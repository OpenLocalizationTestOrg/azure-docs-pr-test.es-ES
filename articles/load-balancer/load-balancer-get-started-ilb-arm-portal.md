---
title: 'aaaCreate un equilibrador de carga interno: portal de Azure | Documentos de Microsoft'
description: "Obtenga información acerca de cómo toocreate un interno equilibrador de carga de recursos Manager mediante Hola portal de Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ac14fb9-8d14-4892-bfe6-8bc74c48ae2c
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 80124217a84857b542eb41cb814ec97234176dd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-in-hello-azure-portal"></a>Crear un equilibrador de carga interno en hello portal de Azure

> [!div class="op_single_selector"]
> * [Azure Portal](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [CLI de Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Plantilla](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).  Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar de hello [modelo de implementación clásica](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a>Primeros pasos en la creación de un equilibrador de carga interno mediante el Portal de Azure

Usar hello siguiendo los pasos toocreate un equilibrador de carga interno de hello Portal de Azure.

1. Abra un explorador, vaya toohello [portal de Azure](http://portal.azure.com)e inicie sesión con su cuenta de Azure.
2. En hello superior izquierda de la pantalla de bienvenida, haga clic en **New** > **red** > **equilibrador de carga**.
3. Hola **equilibrador de carga de crear** hoja, escriba una **nombre** para el equilibrador de carga.
4. En **Esquema**, haga clic en **Interno**.
5. Haga clic en **red Virtual**, y, a continuación, seleccione Hola donde desea que el equilibrador de carga de hello toocreate de red virtual.

   > [!NOTE]
   > Si no ve la red virtual de Hola que desea toouse, compruebe hello **ubicación** se está usando para el equilibrador de carga de Hola y cambia en consecuencia.

6. Haga clic en **subred**y, a continuación, seleccione subred Hola donde desea que el equilibrador de carga de toocreate Hola.
7. En **asignación de direcciones IP**, haga clic en **dinámica** o **estático**, dependiendo de si desea dirección IP de Hola para hello carga equilibrador toobe fijo (estático) o no.

   > [!NOTE]
   > Si selecciona toouse una dirección IP estática, tendrá que tooprovide es una dirección de equilibrador de carga de Hola.

8. En **grupo de recursos** especifique Hola nombre de un nuevo grupo de recursos para el equilibrador de carga de hello, o haga clic en **seleccione existente** y seleccione un grupo de recursos existente.
9. Haga clic en **Crear**.

## <a name="configure-load-balancing-rules"></a>Configuración de las reglas de equilibrio de carga

Después de hello creación de equilibrador de carga, vaya tooconfigure de recurso de equilibrador de carga de toohello lo.
Necesita tooconfigure primero un grupo de direcciones de back-end y un sondeo antes de configurar una regla de equilibrio de carga.

### <a name="step-1-configure-a-back-end-pool"></a>Paso 1: Configuración de un grupo back-end

1. Hola portal de Azure, haga clic en **examinar** > **equilibradores de carga**y, a continuación, haga clic en el equilibrador de carga de Hola que creó anteriormente.
2. Hola **configuración** hoja, haga clic en **grupos back-end**.
3. Hola **grupos de direcciones de back-end** hoja, haga clic en **agregar**.
4. Hola **Agregar grupo back-end** hoja, escriba una **nombre** para el grupo de back-end de hello y, a continuación, haga clic en **Aceptar**.

### <a name="step-2-configure-a-probe"></a>Paso 2: Configuración de un sondeo

1. Hola portal de Azure, haga clic en **examinar** > **equilibradores de carga**y, a continuación, haga clic en el equilibrador de carga de Hola que creó anteriormente.
2. Hola **configuración** hoja, haga clic en **sondeos**.
3. Hola **sondeos** hoja, haga clic en **agregar**.
4. Hola **agregar sondeo** hoja, escriba una **nombre** para la sonda de Hola.
5. En **Protocolo**, seleccione **HTTP** (para sitios web) o **TCP** (para otras aplicaciones basadas en TCP).
6. En **puerto**, especifique Hola puerto toouse al acceder a sondeo Hola.
7. En **ruta de acceso** (para HTTP sondeos solo), especifique hello toouse de ruta de acceso como un sondeo.
8. En **intervalo** especificar con qué frecuencia tooprobe Hola aplicación.
9. En **umbral incorrecto**, especifique cuántos intentos deben generar un error antes de máquina virtual de back-end de hello está marcado como incorrecto.
10. Haga clic en **Aceptar** toocreate sondeo.

### <a name="step-3-configure-load-balancing-rules"></a>Paso 3: Configuración de las reglas de equilibrio de carga

1. Hola portal de Azure, haga clic en **examinar** > **equilibradores de carga**y, a continuación, haga clic en el equilibrador de carga de Hola que creó anteriormente.
2. Hola **configuración** hoja, haga clic en **reglas de equilibrio de carga**.
3. Hola **reglas de equilibrio de carga** hoja, haga clic en **agregar**.
4. Hola **regla de equilibrio de carga de agregar** hoja, escriba una **nombre** de regla de Hola.
5. En **Protocolo**, seleccione **HTTP** (para sitios web) o **TCP** (para otras aplicaciones basadas en TCP).
6. En **puerto**, especificar los clientes de puerto de hello conecten equilibrador de carga de hello tooin.
7. En **puerto back-end**, especifique Hola puerto toobe usa en el bloque de back-end de hello (normalmente, el puerto de equilibrador de carga de Hola y el puerto de back-end de Hola se Hola mismo).
8. En **grupo back-end**, seleccione Hola back-end del grupo que creó anteriormente.
9. En **persistencia de la sesión**, seleccione cómo desea que las sesiones toopersist.
10. En **tiempo de espera de inactividad (minutos)**, especifique el tiempo de espera de inactividad de Hola.
11. En **IP flotante (Direct Server Return)**, haga clic en **Deshabilitado** o **Habilitado**.
12. Haga clic en **OK**.

## <a name="next-steps"></a>Pasos siguientes

[Configuración de un modo de distribución del equilibrador de carga](load-balancer-distribution-mode.md)

[Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga](load-balancer-tcp-idle-timeout.md)

