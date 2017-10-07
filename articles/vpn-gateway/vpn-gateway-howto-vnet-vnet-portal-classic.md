---
title: "Creación de una conexión entre redes virtuales: Clásico: Azure Portal | Microsoft Docs"
description: "Cómo redes juntos tooconnect virtual de Azure con PowerShell y Hola portal de Azure clásico."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: f29c3c091d049ff96cf59f4c28ab86a100bcb5fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-connection-classic"></a>Configuración de una conexión de red virtual a red virtual (clásico)

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

Este artículo muestra cómo toocreate una conexión de puerta de enlace VPN entre redes virtuales. Hello redes virtuales pueden estar en Hola mismo o en distintas regiones y de Hola iguales o distintas suscripciones. pasos de Hello en este artículo aplican hello portal de Azure y el modelo de implementación clásica de toohello. También puede crear esta configuración con una herramienta de implementación diferentes o un modelo de implementación seleccionando una opción diferente de hello lista siguiente:

> [!div class="op_single_selector"]
> * [Portal de Azure](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [CLI de Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Portal de Azure clásico](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Conexión de diferentes modelos de implementación - Azure Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Conexión de diferentes modelos de implementación - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![TooVNet diagrama de conectividad de red virtual](./media/vpn-gateway-howto-vnet-vnet-portal-classic/v2vclassic.png)

## <a name="about-vnet-to-vnet-connections"></a>Acerca de conexiones de red virtual a red virtual

Conectar una red virtual (VNet a VNet) tooanother de red virtual en el modelo de implementación clásica de hello mediante una puerta de enlace VPN es similar tooconnecting una ubicación de sitio de red virtual tooan local. Ambos tipos de conectividad usan un tooprovide de puerta de enlace VPN un túnel seguro mediante IPsec/IKE.

Hola redes virtuales que se conecta puede estar en varias suscripciones y regiones diferentes. Puede combinar la comunicación de red virtual tooVNet con configuraciones de varios sitios. Esto permite establecer topologías de red que combinen la conectividad entre entornos con la conectividad entre redes virtuales.

![TooVNet las conexiones de red virtual](./media/vpn-gateway-howto-vnet-vnet-portal-classic/aboutconnections.png)

### <a name="why"></a>¿Por qué debería conectarse a redes virtuales?

Puede que desee tooconnect las redes virtuales para hello siguientes motivos:

* **Presencia geográfica y redundancia geográfica entre regiones**

  * Puede configurar su propia replicación geográfica o sincronización con conectividad segura sin recurrir a los puntos de conexión a Internet.
  * Con Azure Load Balancer y Microsoft, o con una tecnología de agrupación en clústeres de otros fabricantes, puede configurar cargas de trabajo de alta disponibilidad y redundancia geográfica en varias regiones de Azure. Por ejemplo, puede tooset seguridad SQL Always On con grupos de disponibilidad a través de varias regiones de Azure.
* **Aplicaciones regionales de varios niveles con límite de aislamiento sólido**

  * Hola dentro mismo región, puede configurar aplicaciones de varios niveles con varias redes virtuales conectadas junto con un aislamiento sólido y una comunicación segura entre nivel.
* **Comunicación entre suscripciones y entre organizaciones en Azure**

  * Si tiene varias suscripciones a Azure, puede conectar cargas de trabajo de distintas suscripciones simultáneamente entre redes virtuales de forma segura.
  * Asimismo, tanto las empresas como los proveedores de servicios pueden habilitar la comunicación entre organizaciones con tecnología VPN segura en Azure.

Para obtener más información acerca de las conexiones de red virtual a red virtual, vea [consideraciones de red virtual a red virtual](#faq) final Hola de este artículo.

### <a name="before-you-begin"></a>Antes de empezar

Antes de comenzar este ejercicio, descargue e instale la versión más reciente de Hola de hello cmdlets de PowerShell de administración de servicio de Azure (SM). Para obtener más información, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview). Usamos portal hello para la mayoría de los pasos de hello, pero debe utilizar PowerShell toocreate Hola conexiones entre redes virtuales Hola. No se puede crear conexiones de hello mediante Hola portal de Azure.

## <a name="plan"></a>Paso 1: Planeamiento de los intervalos de direcciones IP

Es importante toodecide intervalos de Hola que podrá usar tooconfigure las redes virtuales. Para esta configuración, debe asegurarse de que ninguno de los intervalos de red virtual se superponen entre sí o con cualquiera de las redes locales de Hola que se conectan.

Hello tabla siguiente muestra un ejemplo de cómo toodefine sus redes virtuales. Usar Hola intervalos solo como directriz. Escriba los intervalos de Hola para las redes virtuales. Necesitará esta información en pasos posteriores.

**Ejemplo**

| Virtual Network | Espacio de direcciones | Region | Se conecta el sitio de red toolocal |
|:--- |:--- |:--- |:--- |
| TestVNet1 |TestVNet1<br>(10.11.0.0/16)<br>(10.12.0.0/16) |Este de EE. UU. |VNet4Local<br>(10.41.0.0/16)<br>(10.42.0.0/16) |
| TestVNet4 |TestVNet4<br>(10.41.0.0/16)<br>(10.42.0.0/16) |Oeste de EE. UU. |VNet1Local<br>(10.11.0.0/16)<br>(10.12.0.0/16) |

## <a name="vnetvalues"></a>Paso 2: crear Hola redes virtuales

Crea dos redes virtuales en hello [portal de Azure](https://portal.azure.com). Para hello pasos toocreate de redes virtuales clásicas, consulte [crear una red virtual clásica](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). 

Cuando se usa Hola portal toocreate una red virtual clásica, debe navegar toohello hoja de red virtual mediante Hola siguiendo los pasos, en caso contrario, no aparece Hola opción toocreate una red virtual clásica:

1. Haga clic en hello '+' hoja 'New' de tooopen Hola.
2. En campo de hello 'Busque en marketplace hello', escriba 'Red Virtual'. Si en su lugar, seleccione las redes -> red Virtual, no podrá obtener Hola opción toocreate una red virtual clásica.
3. Busque 'Red Virtual' de hello devuelve la lista y haga clic en hoja de red Virtual de tooopen Hola. 
4. En la hoja de la red virtual de hello, seleccione 'Clásica' toocreate una red virtual clásica. 

Si usas este artículo como un ejercicio, puede usar Hola después de los valores de ejemplo:

**Valores para TestVNet1**

Nombre: TestVNet1<br>
Espacio de direcciones: 10.11.0.0/16, 10.12.0.0/16 (opcional)<br>
Nombre de subred: predeterminado<br>
Intervalo de direcciones de subred: 10.11.0.1/24<br>
Grupo de recursos: ClassicRG<br>
Ubicación: Este de EE. UU.<br>
GatewaySubnet: 10.11.1.0/27

**Valores para TestVNet4**

Nombre: TestVNet4<br>
Espacio de direcciones: 10.41.0.0/16, 10.42.0.0/16 (opcional)<br>
Nombre de subred: predeterminado<br>
Intervalo de direcciones de subred: 10.41.0.1/24<br>
Grupo de recursos: ClassicRG<br>
Ubicación: Oeste de EE. UU.<br>
GatewaySubnet: 10.41.1.0/27

**Al crear las redes virtuales, tenga en hello cuenta después de configuración:**

* **Espacios de direcciones de red virtual** : en la página de espacios de direcciones de red Virtual de hello, especifique Hola intervalo de direcciones que desea toouse para la red virtual. Se trata de direcciones IP dinámicas Hola que se va a asignar máquinas virtuales de toohello y otras instancias de rol que implemente toothis de red virtual.<br>Hola espacios de direcciones que seleccione no pueden solaparse con espacios de direcciones de Hola para cualquiera de Hola a otras ubicaciones de redes virtuales o locales que va a conectar esta red virtual.

* **Ubicación** : al crear una red virtual, la debe asociar a una ubicación de Azure (región). Por ejemplo, si desea que las máquinas virtuales que están implementan toobe de red virtual tooyour ubicado físicamente en el oeste de Estados Unidos, seleccione esa ubicación. No se puede cambiar la ubicación Hola asociado a la red virtual después de haberlo creado.

**Después de crear las redes virtuales, puede agregar Hola después de configuración:**

* **Espacio de direcciones** : espacio de direcciones adicional no es necesario para esta configuración, pero puede agregar espacio de direcciones adicionales después de crear Hola red virtual.

* **Subredes** : subredes adicionales no son necesarios para esta configuración, pero es recomendable toohave las máquinas virtuales en una subred que es independiente de las demás instancias de rol.

* **Servidores DNS** : escriba el nombre del servidor DNS de Hola y la dirección IP. Mediante este valor no se crea un servidor DNS. Permite a toospecify los servidores DNS Hola que quiere toouse de resolución de nombres para esta red virtual.

En esta sección, configurar el tipo de conexión de hello, sitio local de hello y crear la puerta de enlace de Hola.

## <a name="localsite"></a>Paso 3: configurar el sitio local de Hola

Configuración de Azure usa Hola habían especificado en cada toodetermine de sitio de red local cómo tooroute el tráfico entre redes virtuales Hola. Cada red virtual debe apuntar toohello respectivos red local que desee tooroute el tráfico. Determinar el nombre de Hola que desea que el sitio de red local de toouse toorefer tooeach. Es mejor toouse algo descriptivo.

Por ejemplo, TestVNet1 se conecta tooa sitio de red local que se crea con el nombre 'VNet4Local'. configuración de Hola para VNet4Local contiene prefijos de direcciones de Hola para TestVNet4.

Hola local del sitio para cada red virtual se Hola otra VNet. Después de los valores de ejemplo de Hola sirven para nuestra configuración:

| Virtual Network | Espacio de direcciones | Region | Se conecta el sitio de red toolocal |
|:--- |:--- |:--- |:--- |
| TestVNet1 |TestVNet1<br>(10.11.0.0/16)<br>(10.12.0.0/16) |Este de EE. UU. |VNet4Local<br>(10.41.0.0/16)<br>(10.42.0.0/16) |
| TestVNet4 |TestVNet4<br>(10.41.0.0/16)<br>(10.42.0.0/16) |Oeste de EE. UU. |VNet1Local<br>(10.11.0.0/16)<br>(10.12.0.0/16) |

1. Busque TestVNet1 en hello portal de Azure. Hola **conexiones VPN** sección de hoja de hello, haga clic en **puerta de enlace**.

    ![Sin puerta de enlace](./media/vpn-gateway-howto-vnet-vnet-portal-classic/nogateway.png)
2. En hello **conexión VPN nueva** página, seleccione **sitio a sitio**.
3. Haga clic en **sitio Local** tooopen Hola página del sitio Local y configurar las opciones de Hola.
4. En hello **sitio Local** página, asigne el nombre de su sitio local. En nuestro ejemplo, se asigna el nombre sitio local de hello 'VNet4Local'.
5. Para la **dirección IP de VPN Gateway**, puede usar la dirección IP que desee, siempre que tenga un formato válido. Normalmente, usaría dirección IP externa real Hola para un dispositivo VPN. Sin embargo, para una configuración de red virtual a red virtual clásica, usar dirección IP pública Hola que se asigna la puerta de enlace de toohello para la red virtual. Dado que aún no ha creado la puerta de enlace de red virtual de hello, especifique cualquier dirección IP pública válida como un marcador de posición.<br>No lo deje en blanco: no es opcional para esta configuración. En un paso posterior, vuelva a estos parámetros y configurarlos con direcciones IP en la puerta de enlace de red virtual de hello correspondientes que genera Azure.
6. Para **espacio de direcciones de cliente**, usar espacio de direcciones de Hola de hello otra VNet. Consulte tooyour planeación de ejemplo. Haga clic en **Aceptar** toosave la configuración y el valor devuelto toohello back- **conexión VPN nueva** hoja.

    ![sitio local](./media/vpn-gateway-howto-vnet-vnet-portal-classic/localsite.png)

## <a name="gw"></a>Paso 4: crear la puerta de enlace de red virtual de Hola

Cada red virtual debe tener una puerta de enlace de red virtual. Hola rutas de puerta de enlace de red virtual y cifra el tráfico.

1. En hello **conexión VPN nueva** hoja, seleccione Hola casilla **crear inmediatamente la puerta de enlace**.
2. Haga clic en **Subred, tamaño y tipo de enrutamiento**. En hello **configuración de puerta de enlace** hoja, haga clic en **subred**.
3. nombre de subred de puerta de enlace de Hola se rellena automáticamente con el nombre requerido de Hola "GatewaySubnet". Hola **intervalo de direcciones** contiene direcciones IP de Hola que se asignan los servicios de puerta de enlace VPN toohello. Algunas configuraciones permiten una subred de puerta de enlace de /29, pero su mejor toouse un /28 o /27 tooaccommodate configuraciones futuras que pueden requerir más direcciones IP para los servicios de puerta de enlace de Hola. En la configuración de ejemplo, usamos 10.11.1.0/27. Ajustar el espacio de direcciones de hello, a continuación, haga clic en **Aceptar**.
4. Configurar hello **tamaño de puerta de enlace**. Esta configuración hace referencia toohello [SKU de puerta de enlace](vpn-gateway-about-vpn-gateway-settings.md#gwsku).
5. Configurar hello **tipo de enrutamiento**. Hola tipo de enrutamiento para esta configuración debe ser **dinámica**. No se puede cambiar el tipo de enrutamiento de hello más tarde a menos que anule puerta de enlace de Hola y crea uno nuevo.
6. Haga clic en **Aceptar**.
7. En hello **conexión VPN nueva** hoja, haga clic en **Aceptar** toobegin crear puerta de enlace de red virtual de Hola. Crear una puerta de enlace a menudo puede tardar 45 minutos o más, en función de puerta de enlace de hello seleccionado SKU.

## <a name="vnet4settings"></a>Paso 5: Configuración de las opciones de TestVNet4

Repita los pasos de hello demasiado[crear un sitio local](#localsite) y [crear puerta de enlace de red virtual de hello](#gw) tooconfigure TestVNet4, sustituyendo los valores de hello cuando sea necesario. Si realiza esto como un ejercicio, use hello [valores de ejemplo](#vnetvalues).

## <a name="updatelocal"></a>Paso 6 - sitios locales de Hola de actualización

Una vez creadas las puertas de enlace de red virtual para ambas redes virtuales, debe ajustar los sitios locales de hello **dirección IP de puerta de enlace VPN** valores.

|Nombre de red virtual|Sitio conectado|Dirección IP de la puerta de enlace|
|:--- |:--- |:--- |
|TestVNet1|VNet4Local|Dirección IP de VPN Gateway para TestVNet4|
|TestVNet4|VNet1Local|Dirección IP de VPN Gateway para TestVNet1|

### <a name="part-1---get-hello-virtual-network-gateway-public-ip-address"></a>Parte 1: dirección IP pública de Get hello red virtual puerta de enlace

1. Busque la red virtual en hello portal de Azure.
2. Haga clic en hello tooopen VNet **Introducción** hoja. En la hoja de hello, en **conexiones VPN**, puede ver la dirección IP de hello para la puerta de enlace de red virtual.

  ![Dirección IP pública](./media/vpn-gateway-howto-vnet-vnet-portal-classic/publicIP.png)
3. Copie la dirección IP de Hola. Se usará en la sección siguiente Hola.
4. Repita estos pasos para TestVNet4

### <a name="part-2---modify-hello-local-sites"></a>Parte 2: modificar los sitios locales de Hola

1. Busque la red virtual en hello portal de Azure.
2. En la red virtual de hello **Introducción** hoja, haga clic en el sitio local de Hola.

  ![Sitio local creado](./media/vpn-gateway-howto-vnet-vnet-portal-classic/local.png)
3. En hello **las conexiones VPN de sitio a sitio** hoja, haga clic en nombre de Hola de sitio local de Hola que desea toomodify.

  ![Sitio local abierto](./media/vpn-gateway-howto-vnet-vnet-portal-classic/openlocal.png)
4. Haga clic en hello **sitio Local** que desea toomodify.

  ![modificación de sitio](./media/vpn-gateway-howto-vnet-vnet-portal-classic/connections.png)
5. Hola de actualización **dirección IP de puerta de enlace VPN** y haga clic en **Aceptar** configuración de toosave Hola.

  ![dirección IP de puerta de enlace](./media/vpn-gateway-howto-vnet-vnet-portal-classic/gwupdate.png)
6. Cierre Hola otros módulos.
7. Repita estos pasos para TestVNet4.

## <a name="getvalues"></a>Paso 7: recuperar los valores del archivo de configuración de red de Hola

Al crear redes virtuales clásicas en hello portal de Azure, nombres de Hola que aparecen no es nombre completo de Hola que usas para PowerShell. Por ejemplo, una red virtual que aparece con el nombre de toobe **TestVNet1** en el portal de hello, puede tener un nombre mucho más tiempo en el archivo de configuración de red de Hola. Hello nombre podría ser similar: **grupo ClassicRG TestVNet1**. Al crear las conexiones, es importante toouse valores de hello que se ven en el archivo de configuración de red de Hola.

Hola pasos, se conectará tooyour cuenta de Azure y descarga y presenta Hola red configuración archivo tooobtain Hola valores que son necesarios para las conexiones.

1. Descargue e instale la versión más reciente de Hola de hello cmdlets de PowerShell de administración de servicio de Azure (SM). Para obtener más información, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

2. Abra la consola de PowerShell con derechos elevados y conectar con tooyour cuenta. Usar hello después toohelp de ejemplo que se conecta:

  ```powershell
  Login-AzureRmAccount
  ```

  Compruebe las suscripciones de hello para la cuenta de hello.

  ```powershell
  Get-AzureRmSubscription
  ```

  Si tiene más de una suscripción, seleccione Hola suscripción que desea toouse.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
  ```

  A continuación, usar hello siguiente cmdlet tooadd su tooPowerShell de suscripción de Azure para el modelo de implementación clásica de Hola.

  ```powershell
  Add-AzureAccount
  ```
3. Exportar y ver el archivo de configuración de red de Hola. Cree un directorio en el equipo y, a continuación, exportar el directorio de toohello de archivo de configuración de red de Hola. En este ejemplo, el archivo de configuración de red de Hola se exporta demasiado**C:\AzureNet**.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
4. Abra el archivo hello con nombres de Hola de un editor y la vista de texto para las redes virtuales y sitios. Estos serán nombre hello que usar al crear las conexiones.<br>Los nombres de las redes virtuales aparecen como **VirtualNetworkSite name =**<br>Los nombres de los sitios aparecen como **LocalNetworkSiteRef name =**

## <a name="createconnections"></a>Paso 8: Hola para crear conexiones de puerta de enlace VPN

Cuando se han completado todos los pasos anteriores de hello, puede establecer claves compartidas previamente de IPsec/IKE de Hola y crear la conexión de Hola. Este conjunto de pasos usa PowerShell. No se puede configurar las conexiones de red virtual a red virtual para el modelo de implementación clásica de Hola Hola portal de Azure.

En los ejemplos de hello, tenga en cuenta que una clave compartida de Hola exactamente es Hola igual. siempre debe coincidir con la clave compartida de Hola. Ser seguro tooreplace valores de hello en estos ejemplos con los nombres exactos de Hola para sus redes virtuales y sitios de red Local.

1. Crear hello TestVNet1 tooTestVNet4 conexión.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet1' `
  -LocalNetworkSiteName '17BE5E2C_VNet4Local' -SharedKey A1b2C3D4
  ```
2. Crear hello TestVNet4 tooTestVNet1 conexión.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet4' `
  -LocalNetworkSiteName 'F7F7BFC7_VNet1Local' -SharedKey A1b2C3D4
  ```
3. Espere Hola conexiones tooinitialize. Una vez que se ha inicializado la puerta de enlace de hello, Hola estado es 'Correcto'.

  ```
  Error          :
  HttpStatusCode : OK
  Id             :
  Status         : Successful
  RequestId      :
  StatusCode     : OK
  ```

## <a name="faq"></a>Consideraciones de red virtual a red virtual para redes virtuales clásicas
* redes virtuales de Hello pueden estar en hello suscripciones iguales o distintas.
* redes virtuales de Hello pueden estar en hello mismo o en distintas regiones Azure (ubicaciones).
* Un servicio en la nube o un punto de conexión de equilibrio de carga no puede abarcar varias redes virtuales, aunque estas estén conectadas entre sí.
* La conexión simultánea de varias redes virtuales no requiere dispositivos VPN locales.
* VNet a VNet admite la conexión a Azure Virtual Networks. No admite la conexión de máquinas virtuales o servicios en la nube que no están implementan tooa de red virtual.
* Red virtual a red virtual requiere puertas de enlace de enrutamiento dinámico. No se admiten puertas de enlace de enrutamiento estático de Azure.
* La conectividad de red virtual se puede usar de forma simultánea con VPN de varios sitios. Hay un máximo de 10 túneles VPN para una puerta de enlace VPN de red virtual conectarse tooeither otras redes virtuales o sitios locales.
* Hola espacios de direcciones de redes virtuales de hello y no deben superponerse a sitios de red local a local. Espacios de direcciones superpuestos harán que la creación de hello de redes virtuales o cargar toofail de archivos de configuración netcfg.
* No se admiten los túneles redundantes entre un par de redes virtuales.
* Todos los túneles de VPN para red virtual, incluidas las VPN P2S hello, comparten el ancho de banda disponible de Hola para puerta de enlace VPN de Hola y Hola mismo SLA de tiempo de actividad de puerta de enlace VPN en Azure.
* Tráfico de red virtual a red virtual pasa a través de hello red troncal de Azure.

## <a name="next-steps"></a>Pasos siguientes
Compruebe las conexiones. Consulte [Comprobación de una conexión de VPN Gateway](vpn-gateway-verify-connection-resource-manager.md).
