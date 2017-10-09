---
title: "Conectar redes virtuales clásicas tooAzure VNets el Administrador de recursos: Portal | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una conexión VPN entre clásico redes virtuales y VNets el Administrador de recursos mediante la puerta de enlace VPN y el portal de Hola"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 5a90498c-4520-4bd3-a833-ad85924ecaf9
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: bef63b4e829335b2e1a9434a35ebfe33b4fd7373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-hello-portal"></a>Conectar redes virtuales de diferentes modelos de implementación mediante el portal de Hola

Este artículo muestra cómo tooconnect clásico redes virtuales tooResource Manager VNets tooallow Hola recursos ubicados en hello toocommunicate de modelos de implementación independiente entre sí. pasos de Hello en este artículo usan principalmente Hola portal de Azure, pero también puede crear esta configuración con PowerShell Hola seleccionando artículo Hola de esta lista.

> [!div class="op_single_selector"]
> * [Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

Conectar un tooa de red virtual clásica VNet el Administrador de recursos es similar tooconnecting una ubicación de sitio de red virtual tooan local. Ambos tipos de conectividad usan un tooprovide de puerta de enlace VPN un túnel seguro mediante IPsec/IKE. Puede crear una conexión entre redes virtuales que estén en diferentes suscripciones y en diferentes regiones. También puede conectar redes virtuales que ya tengan redes locales tooon de conexiones, siempre que sea de puerta de enlace de Hola que les ha configurado dinámica o basadas en enrutamiento. Para obtener más información acerca de las conexiones de red virtual a red virtual, vea hello [P+F de red virtual a red virtual](#faq) final Hola de este artículo. 

Si sus redes virtuales están en hello misma región, puede que desee tooinstead considerar realizar la conexión con el intercambio de tráfico de red virtual. El emparejamiento de VNET no usa VPN Gateway. Para más información, consulte [Emparejamiento de VNET](../virtual-network/virtual-network-peering-overview.md). 

### <a name="prerequisites"></a>Requisitos previos

* En estos pasos se presume que ya se crearon ambas redes virtuales. Si está utilizando este artículo como un ejercicio y no tiene redes virtuales, hay vínculos en hello pasos toohelp puede crearlas.
* Compruebe que los intervalos de direcciones de Hola para hello que redes virtuales no se superponen entre sí, o se superponen con ninguno de hello intervalos para otras conexiones que hello las puertas de enlace pueden estar conectados a.
* Instalar cmdlets de PowerShell más recientes de hello para el Administrador de recursos y administración de servicios (clásico). En este artículo, utilizamos Hola portal de Azure y PowerShell. PowerShell es necesario toocreate Hola conexión de hello toohello clásico de red virtual VNet el Administrador de recursos. Para obtener más información, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview). 

### <a name="values"></a>Configuración de ejemplo

Puede usar estos toocreate valores un entorno de prueba, o consulte toothem toobetter comprender los ejemplos de hello en este artículo.

**Red virtual clásica**

Nombre de red virtual = ClassicVNet <br>
Espacio de direcciones = 10.0.0.0/24 <br>
Subred-1 = 10.0.0.0/27 <br>
Grupo de recursos = ClassicRG <br>
Ubicación = Oeste de EE. UU. <br>
GatewaySubnet = 10.0.0.32/28 <br>
Sitio local = RMVNetLocal <br>

**Red virtual de Resource Manager**

Nombre de red virtual = RMVNet <br>
Espacio de direcciones = 192.168.0.0/16 <br>
Subred-1 = 192.168.1.0/24 <br>
Subred de la puerta de enlace = 192.168.0.0/26 <br>
Grupo de recursos = GR1 <br>
Ubicación = Este de EE. UU. <br>
Nombre de la puerta de enlace de red virtual = PuertaDeEnlaceRM <br>
Tipo de puerta de enlace = VPN <br>
Tipo de VPN = basada en enrutamiento <br>
Nombre de dirección IP pública de puerta de enlace = rmgwpip <br>
Puerta de enlace de red local = LocalRedVClásica <br>
Nombre de conexión = RMtoClassic

### <a name="connection-overview"></a>Información general sobre la conexión

Para esta configuración, crea una conexión de puerta de enlace VPN a través de un túnel VPN de IPsec/IKE entre redes virtuales de Hola. Asegúrese de que ninguno de los intervalos de red virtual se superponen entre sí o con cualquiera de las redes locales de Hola que se conectan.

Hello tabla siguiente muestra un ejemplo de cómo se definen el ejemplo hello redes virtuales y sitios locales:

| Virtual Network | Espacio de direcciones | Region | Se conecta el sitio de red toolocal |
|:--- |:--- |:--- |:--- |
| ClassicVNet |(10.0.0.0/24) |Oeste de EE. UU. | RMVNetLocal (192.168.0.0/16) |
| RMVNet | (192.168.0.0/16) |Este de EE. UU. |ClassicVNetLocal (10.0.0.0/24) |

## <a name="classicvnet"></a>1. Configurar opciones de red virtual clásicas de Hola

En esta sección, creará Hola local (sitio local) de red y puerta de enlace de red virtual de hello para la red virtual clásica. Si no tiene una red virtual clásica y se ejecutan estos pasos como un ejercicio, puede crear una red virtual mediante [este artículo](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) hello y [ejemplo](#values) valores de configuración anteriores.

Cuando se usa Hola portal toocreate una red virtual clásica, debe navegar toohello hoja de red virtual mediante Hola siguiendo los pasos, en caso contrario, no aparece Hola opción toocreate una red virtual clásica:

1. Haga clic en hello '+' hoja 'New' de tooopen Hola.
2. En campo de hello 'Busque en marketplace hello', escriba 'Red Virtual'. Si en su lugar, seleccione las redes -> red Virtual, no podrá obtener Hola opción toocreate una red virtual clásica.
3. Busque 'Red Virtual' de hello devuelve la lista y haga clic en hoja de red Virtual de tooopen Hola. 
4. En la hoja de la red virtual de hello, seleccione 'Clásica' toocreate una red virtual clásica. 

Si ya tiene una red virtual con una puerta de enlace VPN, compruebe que esa puerta de enlace de hello es dinámico. Si es estático, primero debe eliminar la puerta de enlace VPN de Hola y continuar.

Las capturas de pantalla se proporcionan a modo de ejemplo. Ser seguro tooreplace valores de hello con su propia o utilizar hello [ejemplo](#values) valores.

### <a name="part-1---configure-hello-local-site"></a>Parte 1: configurar el sitio local de Hola

Abra hello [portal de Azure](https://ms.portal.azure.com) e inicie sesión con su cuenta de Azure.

1. Navegue demasiado**todos los recursos** y busque hello **ClassicVNet** en la lista de Hola.
2. En hello **Introducción** hoja en hello **conexiones VPN** sección, haga clic en hello **puerta de enlace** toocreate gráfico una puerta de enlace.

    ![Configurar una puerta de enlace VPN](./media/vpn-gateway-connect-different-deployment-models-portal/gatewaygraphic.png "Configurar una puerta de enlace VPN")
3. En hello **conexión VPN nueva** hoja, para **tipo de conexión**, seleccione **sitio a sitio**.
4. En **Sitio local**, haga clic en **Configurar los valores obligatorios**. Se abrirá hello **sitio Local** hoja.
5. En hello **sitio Local** hoja, crear un toohello de toorefer VNet el Administrador de recursos de nombre. Por ejemplo, "RMVNetLocal".
6. Si la puerta de enlace VPN de Hola para hello VNet el Administrador de recursos ya tiene una dirección IP pública, utilice el valor de Hola para hello **dirección IP de puerta de enlace VPN** campo. Si lleva a cabo estos pasos como ejercicio o todavía no tiene una puerta de enlace de red virtual para la red virtual de Resource Manager, puede inventar una dirección IP de marcador de posición. Asegúrese de que la dirección IP de marcador de posición de hello usa un formato válido. Más adelante, reemplace dirección IP de marcador de posición de hello con dirección IP pública de puerta de enlace de red virtual de administrador de recursos de Hola Hola.
7. Para **espacio de direcciones de cliente**, utilice valores de hello para espacios de direcciones IP de red virtual de Hola para hello VNet el Administrador de recursos. Esta configuración es toospecify usado Hola dirección espacios tooroute toohello el Administrador de recursos red virtual.
8. Haga clic en **Aceptar** toosave Hola valores y devuelven toohello **conexión VPN nueva** hoja.

### <a name="part-2---create-hello-virtual-network-gateway"></a>Parte 2: crear la puerta de enlace de red virtual de Hola

1. En hello **conexión VPN nueva** hoja, seleccione hello **crear inmediatamente la puerta de enlace** casilla de verificación y haga clic en **configuración opcional de la puerta de enlace** tooopen hello  **Configuración de puerta de enlace** hoja. 

    ![Abrir hoja de configuración de puerta de enlace](./media/vpn-gateway-connect-different-deployment-models-portal/optionalgatewayconfiguration.png "Abrir hoja de configuración de puerta de enlace")
2. Haga clic en **subred - configurar los valores obligatorios** tooopen hello **Agregar subred** hoja. Hola **nombre** ya está configurado con el valor de hello necesario **GatewaySubnet**.
3. Hola **intervalo de direcciones** hace referencia toohello intervalo de subred de puerta de enlace de Hola. Si bien puede crear una subred de puerta de enlace con un intervalo de direcciones de /29 (3 direcciones), se recomienda crear una subred de puerta de enlace que incluya más direcciones IP. Esto permitirá configuraciones futuras que puedan requerir más direcciones IP disponibles. Si es posible, utilice /27 o /28. Si está siguiendo estos pasos como un ejercicio, puede consultar toohello [ejemplo](#values) valores. Haga clic en **Aceptar** subred de puerta de enlace de toocreate Hola.
4. En hello **configuración de puerta de enlace** hoja, **tamaño** hace referencia a la puerta de enlace de toohello SKU. Seleccione la puerta de enlace Hola SKU para la puerta de enlace VPN.
5. Comprobar hello **tipo de enrutamiento** es **dinámica**, a continuación, haga clic en **Aceptar** tooreturn toohello **conexión VPN nueva** hoja.
6. En hello **conexión VPN nueva** hoja, haga clic en **Aceptar** toobegin crear la puerta de enlace VPN. Crear una puerta de enlace VPN puede tardar hasta too45 minutos toocomplete.

### <a name="ip"></a>Parte 3: puerta de enlace de red virtual de hello copia la dirección IP pública

Una vez creada la puerta de enlace de red virtual de hello, puede ver la dirección IP de puerta de enlace de Hola. 

1. Navegue tooyour clásico red virtual y haga clic en **Introducción**.
2. Haga clic en **conexiones VPN** hoja de conexiones VPN de tooopen Hola. En la hoja de conexiones de VPN de hello, puede ver la dirección IP pública Hola. Se trata de una dirección IP pública de hello asignada tooyour puerta de enlace de red virtual. 
3. Escriba o copie la dirección IP de Hola. Se usa en pasos posteriores al trabajar con las opciones de configuración de puerta de enlace de red local de Resource Manager. También puede ver el estado de Hola de las conexiones de puerta de enlace. Sitio de red local de hello aviso que creó aparece como 'Conectar'. estado de Hello cambiará después de crear las conexiones.
4. Cierre la hoja de hello después de copiar la dirección IP de puerta de enlace de Hola.

## <a name="rmvnet"></a>2. Configurar opciones de red virtual del Administrador de recursos de Hola

En esta sección, creará puerta de enlace de red virtual de Hola y puerta de enlace de red local de hello de la VNet del Administrador de recursos. Si no tiene un administrador de recursos de VNet y se ejecutan estos pasos como un ejercicio, puede crear una red virtual mediante [este artículo](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) hello y [ejemplo](#values) valores de configuración anteriores.

Las capturas de pantalla se proporcionan a modo de ejemplo. Ser seguro tooreplace valores de hello con su propia o utilizar hello [ejemplo](#values) valores.

### <a name="part-1---create-a-gateway-subnet"></a>Parte 1: creación de una subred de la puerta de enlace

Antes de crear una puerta de enlace de red virtual, primero debe subred de puerta de enlace de toocreate Hola. Cree una subred de puerta de enlace con un recuento CIDR de /28 o mayor. (/27, /26, etc.)

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

### <a name="part-2---create-a-virtual-network-gateway"></a>Parte 2: creación de una puerta de enlace de la red virtual

[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

### <a name="createlng"></a>Parte 3: creación de una puerta de enlace de la red local

puerta de enlace de red local de Hello especifica el intervalo de direcciones de Hola y dirección IP pública de hello asociada a la red virtual clásica y su puerta de enlace de red virtual.

Si está realizando estos pasos como un ejercicio, consulte Configuración de toothese:

| Virtual Network | Espacio de direcciones | Region | Se conecta el sitio de red toolocal |Dirección IP pública de puerta de enlace|
|:--- |:--- |:--- |:--- |:--- |
| ClassicVNet |(10.0.0.0/24) |Oeste de EE. UU. | RMVNetLocal (192.168.0.0/16) |Hola dirección IP pública que se asigna la puerta de enlace de toohello ClassicVNet|
| RMVNet | (192.168.0.0/16) |Este de EE. UU. |ClassicVNetLocal (10.0.0.0/24) |dirección IP pública que se asigna la puerta de enlace de toohello RMVNet Hola.|

[!INCLUDE [vpn-gateway-add-lng-rm-portal](../../includes/vpn-gateway-add-lng-rm-portal-include.md)]

## <a name="modifylng"></a>3. Modificar configuración del sitio local de red virtual clásica de Hola

En esta sección, reemplace dirección IP de marcador de posición de Hola que usó al especificar la configuración de sitio local de hello, con hello dirección IP de puerta de enlace de VPN de administrador de recursos. Esta sección utiliza Hola clásicos cmdlets de PowerShell (SM).

1. Hola portal de Azure, navegue toohello de red virtual clásica.
2. En la hoja de hello para la red virtual, haga clic en **Introducción**.
3. Hola **conexiones VPN** sección, haga clic en nombre de Hola de su sitio local en el gráfico de Hola.

    ![Conexiones VPN](./media/vpn-gateway-connect-different-deployment-models-portal/vpnconnections.png "Conexiones VPN")
4. En hello **conexiones VPN de sitio a sitio** hoja, haga clic en nombre de hello del sitio de Hola.

    ![Nombre del sitio](./media/vpn-gateway-connect-different-deployment-models-portal/sitetosite3.png "Nombre del sitio local")
5. En la hoja de conexión de hello para el sitio local, haga clic en nombre de Hola de Hola Hola de tooopen de sitio local **sitio Local** hoja.

    ![Abrir sitio local](./media/vpn-gateway-connect-different-deployment-models-portal/openlocal.png "Abrir sitio local")
6. En hello **sitio Local** hoja, replace hello **dirección IP de puerta de enlace VPN** con la dirección IP de Hola de puerta de enlace de hello Administrador de recursos.

    ![Dirección IP de puerta de enlace](./media/vpn-gateway-connect-different-deployment-models-portal/gwipaddress.png "Dirección IP de puerta de enlace")
7. Haga clic en **Aceptar** dirección IP de tooupdate Hola.

## <a name="RMtoclassic"></a>4. Crear conexiones de administrador de recursos tooclassic

En estos pasos, configurar conexión Hola de hello VNet Administrador de recursos del uso de red virtual clásica toohello Hola portal de Azure.

1. En **todos los recursos**, busque la puerta de enlace de red local de Hola. En nuestro ejemplo, es la puerta de enlace de red local de hello **ClassicVNetLocal**.
2. Haga clic en **configuración** y compruebe que el valor de dirección IP de hello es puerta de enlace VPN de Hola para hello clásico red virtual. Actualice si es necesario y, luego, haga clic en **Guardar**. Hoja de hello cerrar.
3. En **todos los recursos**, haga clic en puerta de enlace de red local de Hola.
4. Haga clic en **conexiones** hoja de tooopen hello las conexiones.
5. En hello **conexiones** hoja, haga clic en  **+**  tooadd una conexión.
6. En hello **Agregar conexión** hoja, nombre de la conexión Hola. Por ejemplo, "RMtoClassic".
7. En esta hoja ya está seleccionada la opción **De sitio a sitio**.
8. Seleccione Hola de puerta de enlace de red virtual que desea tooassociate con este sitio.
9. Cree una **clave compartida**. Esta clave también se utiliza en la conexión de Hola que se crea desde toohello de red virtual clásica de hello VNet el Administrador de recursos. Puede generar clave de Hola o forman uno. En el ejemplo usamos "abc123", pero puede (y debe) usar un valor más complejo.
10. Haga clic en **Aceptar** conexión de hello toocreate.

##<a name="classictoRM"></a>5. Crear tooResource clásico de connection Manager

En estos pasos, configura conexión de Hola de hello toohello clásico de red virtual VNet el Administrador de recursos. Estos pasos requieren PowerShell. No se puede crear esta conexión en el portal de Hola. Asegúrese de que ha descargado e instalado Hola clásico (SM) y cmdlets de PowerShell del Administrador de recursos (RM).

### <a name="1-connect-tooyour-azure-account"></a>1. Conectar tooyour cuenta de Azure

Abra la consola de PowerShell de hello con derechos elevados e inicie sesión tooyour cuenta de Azure. Hello siguiente cmdlet le pide las credenciales de inicio de sesión de Hola para su cuenta de Azure. Después de iniciar sesión, la configuración de su cuenta se descarga para que estén disponible tooAzure PowerShell.

```powershell
Login-AzureRmAccount
```
   
Si tiene más de una suscripción de Azure, obtenga una lista de todas ellas.

```powershell
Get-AzureRmSubscription
```

Especifique que desea toouse de suscripción de Hola. 

```powershell
Select-AzureRmSubscription -SubscriptionName "Name of subscription"
```

Agregue los cuenta de Azure toouse Hola clásico los cmdlets de PowerShell (SM). toodo por lo tanto, puede usar Hola siguiente comando:

```powershell
Add-AzureAccount
```

### <a name="2-view-hello-network-configuration-file-values"></a>2. Ver valores de archivo de configuración de red de Hola

Cuando se crea una red virtual en hello portal de Azure, nombre completo de Hola que utiliza Azure no está visible en hello portal de Azure. Por ejemplo, una red virtual que aparece toobe denominado 'ClassicVNet' Hola portal de Azure puede tener un nombre mucho más tiempo en el archivo de configuración de red de Hola. Hello nombre podría ser similar: 'Grupo ClassicRG ClassicVNet'. En estos pasos, descargue Hola red archivo y ver Hola valores de configuración.

Cree un directorio en el equipo y, a continuación, exportar el directorio de toohello de archivo de configuración de red de Hola. En este ejemplo, el archivo de configuración de red de hello es tooC:\AzureNet exportado.

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

Abra el archivo hello con un nombre de hello del editor y la vista de texto para la red virtual clásica. Utilice nombres de hello en el archivo de configuración de red de hello al ejecutar los cmdlets de PowerShell.

- Los nombres de las redes virtuales aparecen como **VirtualNetworkSite name =**
- Los nombres de los sitios aparecen como **LocalNetworkSite name=**

### <a name="3-create-hello-connection"></a>3. Crear conexiones de Hola

Configurar la clave compartida de Hola y crear la conexión de Hola de hello toohello clásico de red virtual VNet el Administrador de recursos. No se puede establecer una clave compartida hello mediante el portal de Hola. Asegúrese de que se ejecute estos pasos mientras haya iniciado sesión con la versión clásica de Hola de hello cmdlets de PowerShell. por lo tanto, use toodo **Add-AzureAccount**. En caso contrario, no será capaz de tooset hello '-AzureVNetGatewayKey'.

- En este ejemplo, **- VNetName** es el nombre de Hola de hello clásico red virtual como se encuentra en el archivo de configuración de red. 
- Hola **- LocalNetworkSiteName** se encuentra especificado para el sitio local de hello, como el nombre de hello en el archivo de configuración de red.
- Hola **- SharedKey** es un valor que se generan y se especifica. En este ejemplo, hemos utilizado *abc123* pero puede generar algo más complejo. Hola importante que es ese valor de Hola que especifique aquí debe ser Hola que mismo valor que especificó al crear la conexión de administrador de recursos tooclassic.

```powershell
Set-AzureVNetGatewayKey -VNetName "Group ClassicRG ClassicVNet" `
-LocalNetworkSiteName "172B9E16_RMVNetLocal" -SharedKey abc123
```

##<a name="verify"></a>6. Comprobación de las conexiones

Puede comprobar que las conexiones mediante el uso de Hola portal de Azure o PowerShell. Al comprobar, puede que necesite toowait un minuto o dos tal y como se va a crear la conexión de Hola. Cuando una conexión se realiza correctamente, el estado de conectividad de hello cambia de 'Conectar' too'Connected'.

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a>conexión de hello tooverify desde su tooyour clásico de red virtual VNet el Administrador de recursos

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

###<a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a>conexión de hello tooverify desde el Administrador de recursos VNet tooyour red virtual clásica

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="faq"></a>P+F sobre conexiones de red virtual a red virtual

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]
