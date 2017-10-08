---
title: "aaaCreate una puerta de enlace de la aplicación: Portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una puerta de enlace de la aplicación mediante el uso de Hola portal"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 54dffe95-d802-4f86-9e2e-293f49bd1e06
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 24c1d5701eae372cd233162ceb58dea36a3b6a39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-hello-portal"></a>Crear una puerta de enlace de la aplicación con el portal de Hola

[Application Gateway](application-gateway-introduction.md) es una aplicación virtual dedicada que cuenta con un controlador de entrega de aplicaciones (ADC) que se ofrece como servicio y que proporciona numerosas funcionalidades de equilibrio de carga de nivel 7 para una aplicación. En este artículo le guiará Hola pasos toocreate una puerta de enlace de aplicación de uso de hello portal de Azure y agregar un servidor existente como un miembro de back-end.

## <a name="log-in-tooazure"></a>Inicie sesión en tooAzure

Inicie sesión en toohello portal de Azure en [http://portal.azure.com](http://portal.azure.com)

## <a name="create-application-gateway"></a>Creación de una puerta de enlace de aplicaciones

toocreate una puerta de enlace de aplicaciones, Hola completa los pasos siguientes. La puerta de enlace de aplicaciones requiere su subred propia. Al crear una red virtual, asegúrese de dejar suficiente toohave de espacio de direcciones en varias subredes. Una vez puerta de enlace de aplicaciones de hello tooa implementado subred, se pueden agregar solo otras puertas de enlace de aplicaciones tooit.

1. En panel de favoritos de Hola de portal de hello, haga clic en **nuevo**
1. Hola **New** hoja, haga clic en **red**. Hola **red** hoja, haga clic en **Application Gateway**, tal y como se muestra en hello después de imagen:

    ![Creación de una puerta de enlace de aplicaciones][1]

1. Hola **Fundamentos** hoja que aparece, escriba Hola después de valores, a continuación, haga clic en **Aceptar**:

   | **Configuración** | **Valor** | **Detalles**|
   |---|---|---|
   |**Name**|AdatumAppGateway|nombre de Hola de puerta de enlace de aplicación Hola|
   |**Nivel**|Estándar|Los valores disponibles son Estándar y WAF. Visite [firewall de aplicación web](application-gateway-web-application-firewall-overview.md) toolearn más información sobre WAFS.|
   |**Tamaño de la SKU**|Mediano|Las opciones al elegir el nivel Estándar son pequeño, mediano y grande. Al elegir el nivel de WAF, las opciones solo son mediano y grande.|
   |**Recuento de instancias**|2|Número de instancias de puerta de enlace de aplicaciones de Hola para lograr alta disponibilidad. Los recuentos de instancias de 1 solo deben usarse para fines de pruebas.|
   |**Suscripción**|[Su suscripción]|Seleccione una puerta de enlace de suscripción toocreate Hola aplicación en.|
   |**Grupos de recursos**|**Crear nuevo:** AdatumAppGatewayRG|Cree un grupo de recursos. nombre de grupo de recursos de Hello debe ser único dentro de la suscripción de Hola que ha seleccionado. más información acerca de los grupos de recursos, leer hello toolearn [el Administrador de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) artículo de información general.|
   |**Ubicación**|Oeste de EE. UU.||

1. Hola **configuración** hoja que aparece bajo **red Virtual**, haga clic en **elegir una red virtual**. Hola **red virtual de elegir** abre la hoja.  Haga clic en **crear nuevo** tooopen hello **crear red virtual** hoja.

   ![Elegir una red virtual][2]

1. En hello **Crear hoja de red virtual** escriba Hola después de valores, a continuación, haga clic en **Aceptar**. Hola **crear red virtual** y **red virtual de elegir** hojas de cierre. Este paso rellena hello **subred** campo hello **configuración** hoja con subred Hola elegido.

   | **Configuración** | **Valor** | **Detalles**|
   |---|---|---|
   |**Name**|AdatumAppGatewayVNET|Nombre de puerta de enlace de aplicación Hola|
   |**Espacio de direcciones**|10.0.0.0/16|Se trata de espacio de direcciones de hello para la red virtual de Hola|
   |**Nombre de subred**|AppGatewaySubnet|Nombre de subred de Hola para puerta de enlace de aplicación Hola|
   |**Intervalo de direcciones de subred**|10.0.0.0/28|Esta subred permite más subredes adicionales en la red virtual de Hola para los miembros del grupo back-end|

1. En hello **configuración** hoja bajo **configuración Frontend IP**, elija **público** como hello **tipo de dirección IP**

1. En hello **configuración** hoja bajo **dirección IP pública** haga clic en **elegir una dirección IP pública**, hello **Elegir dirección IP pública** abre la hoja , haga clic en **crear nuevo**.

   ![Elegir una dirección IP pública][3]

1. En hello **Crear dirección IP pública** hoja, acepte el valor predeterminado de Hola y haga clic en **Aceptar**. hoja de Hola se cierra y rellena hello **dirección IP pública** con la dirección IP pública Hola elegida.

1. En hello **configuración** hoja bajo **configuración de agente de escucha**, haga clic en **HTTP** en **protocolo**. Escriba Hola puerto toouse Hola **puerto** campo.

2. Haga clic en **Aceptar** en hello **configuración** toocontinue de hoja.

1. Revisar la configuración de hello en hello **resumen** hoja y haga clic en **Aceptar** toostart creación de puerta de enlace de aplicación Hola. Crear una puerta de enlace de la aplicación es una tarea de ejecución prolongada y toma toocomplete de tiempo.

## <a name="add-servers-toobackend-pools"></a>Adición de grupos de servidores toobackend

Una vez creada la puerta de enlace de aplicaciones de hello, sistemas de Hola que hospedan con equilibrio de carga de hello aplicación toobe todavía deben puerta de enlace de aplicaciones de toobe toohello agregada. direcciones IP de Hello, FQDN o NIC de estos servidores se agregan grupos de direcciones de back-end de toohello.

### <a name="ip-address-or-fqdn"></a>Dirección IP o FQDN

1. Con puerta de enlace de aplicaciones de hello creado, en el portal de Azure hello **favoritos** panel, haga clic en **todos los recursos**. Haga clic en hello **AdatumAppGateway** puerta de enlace de aplicaciones en Hola a todos los módulos de recursos. Si la suscripción de Hola que ha seleccionado ya tiene varios recursos en ella, puede escribir **AdatumAppGateway** en hello **filtrar por nombre...** puerta de enlace de cuadro tooeasily acceso Hola aplicaciones.

1. se muestra la puerta de enlace de aplicaciones de Hola que creó. Haga clic en **grupos back-end**y seleccione el grupo actual de back-end de hello **appGatewayBackendPool**, hello **appGatewayBackendPool** abre la hoja.

   ![Grupos de back-end de Application Gateway][4]

1. Haga clic en **Add Target** tooadd las direcciones IP de los valores de FQDN. Elija **IP dirección IP o FQDN** como hello **tipo** y escriba la dirección IP o FQDN en el campo de Hola. Repita este paso para los miembros adicionales del grupo de back-end. Cuando termine, haga clic en **Guardar**.

### <a name="virtual-machine-and-nic"></a>Máquina virtual y NIC

También puede agregar NIC de máquinas virtuales como miembros del grupo de back-end. Solo las máquinas virtuales dentro de la misma red virtual que Hola puerta de enlace de aplicaciones están disponibles a través de Hola Hola lista desplegable.

1. Con puerta de enlace de aplicaciones de hello creado, en el portal de Azure hello **favoritos** panel, haga clic en **todos los recursos**. Haga clic en hello **AdatumAppGateway** puerta de enlace de aplicaciones en Hola a todos los módulos de recursos. Si la suscripción de Hola que ha seleccionado ya tiene varios recursos en ella, puede escribir **AdatumAppGateway** en hello **filtrar por nombre...** puerta de enlace de cuadro tooeasily acceso Hola aplicaciones.

1. se muestra la puerta de enlace de aplicaciones de Hola que creó. Haga clic en **grupos back-end**y seleccione el grupo actual de back-end de hello **appGatewayBackendPool**, hello **appGatewayBackendPool** abre la hoja.

   ![Grupos de back-end de Application Gateway][5]

1. Haga clic en **Add Target** tooadd las direcciones IP de los valores de FQDN. Elija **Máquina Virtual** como hello **tipo** y seleccione la máquina virtual de Hola y toouse NIC. Cuando termine, haga clic en **Guardar**.

   > [!NOTE]
   > Solo las máquinas virtuales en Hola misma red virtual como puerta de enlace de aplicaciones de hello están disponibles en el cuadro desplegable Hola.

## <a name="clean-up-resources"></a>Limpieza de recursos

Cuando ya no es necesario, eliminar el grupo de recursos de hello, puerta de enlace de aplicación y todos los recursos relacionados. toodo seleccione por lo tanto, el grupo de recursos de Hola de hoja de puerta de enlace de aplicaciones de Hola y haga clic en **eliminar**.

## <a name="next-steps"></a>Pasos siguientes

En este escenario, implementar una puerta de enlace de la aplicación y agrega un back-end de servidor toohello. pasos siguientes Hola son tooconfigure puerta de enlace de aplicaciones de hello mediante la modificación de la configuración y reglas de ajustes de puerta de enlace de Hola. Estos pasos pueden encontrarse visitando Hola siguientes artículos:

Obtenga información acerca de cómo sondeos de estado personalizado de toocreate visitando [crear un sondeo de estado personalizados](application-gateway-create-probe-portal.md)

Obtenga información acerca de cómo tooconfigure la descarga de SSL y descifrado de SSL costoso de toman Hola desactivado los servidores web visitando [configurar la descarga de SSL](application-gateway-ssl-portal.md)

Obtenga información acerca de cómo tooprotect las aplicaciones con [Firewall de aplicación Web](application-gateway-webapplicationfirewall-overview.md) una característica de puerta de enlace de aplicaciones.

<!--Image references-->
[1]: ./media/application-gateway-create-gateway-portal/figure1.png
[2]: ./media/application-gateway-create-gateway-portal/figure2.png
[3]: ./media/application-gateway-create-gateway-portal/figure3.png
[4]: ./media/application-gateway-create-gateway-portal/figure4.png
[5]: ./media/application-gateway-create-gateway-portal/figure5.png
[scenario]: ./media/application-gateway-create-gateway-portal/scenario.png
