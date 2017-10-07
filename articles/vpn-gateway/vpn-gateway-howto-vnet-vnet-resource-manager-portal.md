---
title: 'Conectar una red virtual de tooanother de red virtual de Azure: Portal | Documentos de Microsoft'
description: "Crear una conexión de puerta de enlace VPN entre redes virtuales mediante el Administrador de recursos y Hola portal de Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a7015cfc-764b-46a1-bfac-043d30a275df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: a529f90d976bee0f50403947d06e9da8a6c05349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-hello-azure-portal"></a>Configurar una conexión de puerta de enlace VPN de red virtual a red virtual mediante Hola portal de Azure

Este artículo muestra cómo toocreate una conexión de puerta de enlace VPN entre redes virtuales. Hello redes virtuales pueden estar en Hola mismo o en distintas regiones y de Hola iguales o distintas suscripciones. Al conectar redes virtuales de distintas suscripciones, las suscripciones de hello no es necesario toobe asociada Hola a mismo inquilino de Active Directory. 

pasos de Hello en este artículo aplican toohello modelo de implementación del Administrador de recursos y usar hello portal de Azure. También puede crear esta configuración con una herramienta de implementación diferentes o un modelo de implementación seleccionando una opción diferente de hello lista siguiente:

> [!div class="op_single_selector"]
> * [Portal de Azure](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [CLI de Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Portal de Azure clásico](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Conexión de diferentes modelos de implementación - Azure Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Conexión de diferentes modelos de implementación - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![diagrama de v2v](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v2vrmps.png)

Conectar una red virtual (VNet a VNet) tooanother de red virtual es similar tooconnecting una ubicación de sitio de red virtual tooan local. Ambos tipos de conectividad usan un tooprovide de puerta de enlace VPN un túnel seguro mediante IPsec/IKE. Si sus redes virtuales están en hello misma región, puede que desee tooconsider conectándolos mediante el intercambio de tráfico de red virtual. El emparejamiento de VNET no usa VPN Gateway. Para más información, consulte [Emparejamiento de VNET](../virtual-network/virtual-network-peering-overview.md).

Se puede combinar la comunicación entre redes virtuales con configuraciones de varios sitios. Esto le permite establecer topologías de red que combinen la conectividad entre entornos con conectividad entre redes virtuales, como se muestra en hello siguiente diagrama:

![Acerca de las conexiones](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/aboutconnections.png "Acerca de las conexiones")

### <a name="why-connect-virtual-networks"></a>¿Por qué debería conectarse a redes virtuales?

Puede que desee tooconnect las redes virtuales para hello siguientes motivos:

* **Presencia geográfica y redundancia geográfica entre regiones**
  
  * Puede configurar su propia replicación geográfica o sincronización con conectividad segura sin recurrir a los puntos de conexión a Internet.
  * Con el Equilibrador de carga y el Administrador de tráfico de Azure, puede configurar cargas de trabajo de alta disponibilidad con redundancia geográfica en varias regiones de Azure. Por ejemplo, puede tooset seguridad SQL Always On con grupos de disponibilidad a través de varias regiones de Azure.
* **Aplicaciones regionales de niveles múltiples con aislamiento o un límite administrativo**
  
  * Hola dentro mismo región, puede configurar aplicaciones de varios niveles con varias redes virtuales conectadas entre sí debido tooisolation o requisitos administrativos.

Para obtener más información acerca de las conexiones de red virtual a red virtual, vea hello [P+F de red virtual a red virtual](#faq) final Hola de este artículo. Tenga en cuenta que si sus redes virtuales se encuentran en distintas suscripciones, no se puede crear conexiones de hello en el portal de Hola. Puede usar [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) o [CLI](vpn-gateway-howto-vnet-vnet-cli.md).

### <a name="values"></a>Configuración de ejemplo

Al usar estos pasos como un ejercicio, puede utilizar valores de configuración de ejemplo de Hola. En los ejemplos, usamos varios espacios de direcciones para cada red virtual. Sin embargo, las configuraciones de red virtual a red virtual no requieren varios espacios de direcciones.

**Valores para TestVNet1:**

* Nombre de red virtual: TestVNet1
* Espacio de direcciones: 10.11.0.0/16
  * Nombre de subred: FrontEnd
  * Intervalo de direcciones de subred: 10.11.0.0/24
* Grupo de recursos: TestRG1
* Ubicación: Este de EE. UU.
* Espacio de direcciones: 10.12.0.0/16
  * Nombre de subred: BackEnd
  * Intervalo de direcciones de subred: 10.12.0.0/24
* Nombre de subred de puerta de enlace: GatewaySubnet (Esto configurará rellenado automático en el portal de hello)
  * Intervalo de direcciones de subred de puerta de enlace: 10.11.255.0/27
* Servidor DNS: Usar la dirección IP de saludo del servidor DNS
* Nombre de la puerta de enlace de red virtual: TestVNet1GW
* Tipo de puerta de enlace: VPN
* Tipo de VPN: basada en rutas
* SKU: Seleccione Hola SKU de puerta de enlace que desee toouse
* Nombre de dirección IP pública: TestVNet1GWIP
* Valores de conexión:
  * Nombre: TestVNet1toTestVNet4
  * Clave compartida: puede crear una clave compartida Hola. En este ejemplo, usaremos abc123. Hola importante que es que al crear conexión Hola entre redes virtuales hello, Hola valor debe coincidir con.

**Valores para TestVNet4:**

* Nombre de red virtual: TestVNet4
* Espacio de direcciones: 10.41.0.0/16
  * Nombre de subred: FrontEnd
  * Intervalo de direcciones de subred: 10.41.0.0/24
* Grupo de recursos: TestRG1
* Ubicación: Oeste de EE. UU.
* Espacio de direcciones: 10.42.0.0/16
  * Nombre de subred: BackEnd
  * Intervalo de direcciones de subred: 10.42.0.0/24
* Nombre de GatewaySubnet: GatewaySubnet (Esto configurará rellenado automático en el portal de hello)
  * Intervalo de direcciones de GatewaySubnet: 10.41.255.0/27
* Servidor DNS: Usar la dirección IP de saludo del servidor DNS
* Nombre de puerta de enlace de red virtual: TestVNet4GW
* Tipo de puerta de enlace: VPN
* Tipo de VPN: basada en rutas
* SKU: Seleccione Hola SKU de puerta de enlace que desee toouse
* Nombre de dirección IP pública: TestVNet4GWIP
* Valores de conexión:
  * Nombre: TestVNet4toTestVNet1
  * Clave compartida: puede crear una clave compartida Hola. En este ejemplo, usaremos abc123. Hola importante que es que al crear conexión Hola entre redes virtuales hello, Hola valor debe coincidir con.

## <a name="CreatVNet"></a>1. Creación y configuración de TestVNet1
Si ya tiene una red virtual, compruebe que la configuración de hello es compatible con el diseño de la puerta de enlace VPN. Preste especial atención tooany subredes que se pueden superponer con otras redes. Si tiene subredes superpuestas, la conexión no funcionará correctamente. Si la red virtual se configura con la configuración correcta de hello, puede empezar con los pasos de Hola Hola [especifica un servidor DNS](#dns) sección.

### <a name="toocreate-a-virtual-network"></a>toocreate una red virtual
[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-rm-portal-include.md)]

## <a name="subnets"></a>2. Incorporación de un espacio de direcciones adicional y creación de subredes
Una vez que la red virtual se haya creado, puede agregar un espacio de direcciones adicional y crear subredes.

[!INCLUDE [vpn-gateway-additional-address-space](../../includes/vpn-gateway-additional-address-space-include.md)]

## <a name="gatewaysubnet"></a>3. Creación de una subred de puerta de enlace
Antes de conectar la puerta de enlace de red virtual tooa, primero debe subred de puerta de enlace de toocreate Hola Hola toowhich de red virtual se desea tooconnect. Si es posible, es mejor toocreate una subred de puerta de enlace con un bloque CIDR de /28 o /27 en orden tooprovide suficiente IP direcciones tooaccommodate requisitos de configuración futura adicional.

Si va a crear esta configuración como un ejercicio, consulte toothese [configuraciones de ejemplo](#values) al crear la subred de puerta de enlace.

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="toocreate-a-gateway-subnet"></a>toocreate una subred de puerta de enlace
[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

## <a name="dns"></a>4. Especificación de un servidor DNS (opcional)
No se requiere la DNS para las conexiones de red virtual a red virtual. Sin embargo, si desea toohave la resolución de nombres para los recursos de red virtual tooyour implementada, debe especificar un servidor DNS. Esta opción permite especificar el servidor DNS de Hola que quiere toouse de resolución de nombres para esta red virtual. No crea un servidor DNS.

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="VNetGateway"></a>5. Creación de una puerta de enlace de red virtual
En este paso, creará la puerta de enlace de red virtual de hello para la red virtual. Crear una puerta de enlace a menudo puede tardar 45 minutos o más, en función de puerta de enlace de hello seleccionado SKU. Si va a crear esta configuración como un ejercicio, puede consultar toohello [configuraciones de ejemplo](#values).

### <a name="toocreate-a-virtual-network-gateway"></a>toocreate una puerta de enlace de red virtual
[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

## <a name="CreateTestVNet4"></a>6. Creación y configuración de TestVNet4
Una vez haya configurado TestVNet1, cree TestVNet4 repitiendo los pasos anteriores hello, reemplazando los valores de hello con los de TestVNet4. No es necesario toowait hasta que la puerta de enlace de red virtual de Hola para TestVNet1 ha terminado de crear antes de configurar TestVNet4. Si utiliza sus propios valores, asegúrese de que no se superponen con espacios de direcciones de hello con cualquiera de hello redes virtuales que desee tooconnect a.

## <a name="TestVNet1Connection"></a>7. Configurar conexión de hello TestVNet1
Cuando se hayan completado las puertas de enlace de red virtual de Hola para TestVNet1 y TestVNet4, puede crear conexiones de puerta de enlace a la red virtual. En esta sección, creará una conexión de VNet1 tooVNet4. Estos pasos sólo funcionan para redes virtuales en hello misma suscripción. Si sus redes virtuales se encuentran en distintas suscripciones, debe usar conexión de PowerShell toomake Hola. Vea hello [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) artículo.

1. En **todos los recursos**, navegar por la puerta de enlace de red virtual de toohello para la red virtual. Por ejemplo, **TestVNet1GW**. Haga clic en **TestVNet1GW** hoja de puerta de enlace de red virtual de tooopen Hola.
   
    ![Hoja de conexiones](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/settings_connection.png "Hoja de conexiones")
2. Haga clic en **+ agregar** tooopen hello **Agregar conexión** hoja.
3. En hello **Agregar conexión** hoja, en el campo de nombre de hello, escriba un nombre para la conexión. Por ejemplo, **TestVNet1toTestVNet4**.
   
    ![Nombre de conexión](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v1tov4.png "Nombre de conexión")
4. En **Tipo de conexión**, Seleccione **VNet a VNet** de lista desplegable de Hola.
5. Hola **primera puerta de enlace de red virtual** valor del campo se rellena automáticamente porque va a crear esta conexión de puerta de enlace de red virtual especificado de Hola.
6. Hola **segunda puerta de enlace de red virtual** campo es de puerta de enlace de red virtual de Hola de hello red virtual que desea toocreate una conexión. Haga clic en **elegir otra puerta de enlace de red virtual** tooopen hello **puerta de enlace de red virtual de elegir** hoja.
   
    ![Agregar conexión](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/add_connection.png "Agregar una conexión")
7. Vista Hola red virtual puertas de enlace que se muestran en esta hoja. Observe que solo se muestran las que se encuentran en su suscripción. Si desea que la puerta de enlace de la red virtual de tooa de tooconnect que no es de su suscripción, use hello [PowerShell artículo](vpn-gateway-vnet-vnet-rm-ps.md). 
8. Haga clic en la puerta de enlace de red virtual de Hola que desee tooconnect a.
9. Hola **clave compartida** , escriba una clave compartida para la conexión. Dicha clave puede generarla o crearla manualmente. En una conexión de sitio a sitio, clave Hola que utiliza podría ser exactamente Hola mismo para el dispositivo local y la conexión de puerta de enlace de red virtual. concepto de Hello es similar, salvo que en lugar de dispositivo VPN con conexión tooa, que se está conectando tooanother puerta de enlace de red virtual.
   
    ![Clave compartida](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/sharedkey.png "Clave compartida")
10. Haga clic en **Aceptar** en Hola parte inferior de hello hoja toosave los cambios.

## <a name="TestVNet4Connection"></a>8. Configurar conexión de hello TestVNet4
A continuación, cree una conexión de TestVNet4 tooTestVNet1. Use Hola mismo método que usa conexión de hello toocreate de TestVNet1 tooTestVNet4. Asegúrese de que usa Hola misma clave compartida.

## <a name="VerifyConnection"></a>9. Comprobación de la conexión
Compruebe la conexión de Hola. Para cada puerta de enlace de red virtual, Hola siguientes:

1. Busque la hoja de Hola para puerta de enlace de red virtual de Hola. Por ejemplo, **TestVNet4GW**. 
2. En la hoja de la puerta de enlace de red virtual de hello, haga clic en **conexiones** tooview hoja de conexiones de Hola para puerta de enlace de red virtual de Hola.

Ver las conexiones de Hola y comprobar el estado de Hola. Una vez creada la conexión de hello, verá **correcto** y **conectado** como Hola valores de estado.

![Correcto](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/connected.png "Correcto")

Hacer doble clic en cada conexión por separado tooview obtener más información acerca de la conexión de Hola.

![Essentials](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/essentials.png "Essentials")

## <a name="faq"></a>P+F sobre conexiones de red virtual a red virtual
Ver detalles de hello preguntas más frecuentes para obtener información adicional acerca de las conexiones de red virtual a red virtual.

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Pasos siguientes
Una vez completada la conexión, puede agregar redes virtuales de máquinas virtuales tooyour. Vea hello [documentación de máquinas virtuales](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) para obtener más información.
