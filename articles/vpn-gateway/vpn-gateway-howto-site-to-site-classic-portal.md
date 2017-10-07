---
title: "Conectar su tooan de red local red virtual de Azure: VPN de sitio a sitio (clásico): Portal | Documentos de Microsoft"
description: "Una conexión de IPsec desde el entorno local de red tooan red virtual de Azure a través de toocreate de pasos Hola Internet pública. Estos pasos le ayudarán a crear una conexión de puerta de enlace VPN de sitio a sitio entre entornos mediante el portal de Hola."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/010/2017
ms.author: cherylmc
ms.openlocfilehash: b260bdf610b264458660b278bd32bf0fc5b519ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-using-hello-azure-portal-classic"></a>Crear una conexión de sitio a sitio mediante Hola portal de Azure (clásico)

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

Este artículo muestra cómo toouse Hola toocreate portal Azure una conexión de puerta de enlace VPN de sitio a sitio desde su toohello de red local red virtual. pasos de Hello en este artículo aplican toohello modelo de implementación clásica. También puede crear esta configuración con una herramienta de implementación diferentes o un modelo de implementación seleccionando una opción diferente de hello lista siguiente:

> [!div class="op_single_selector"]
> * [Portal de Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portal de Azure clásico](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

Una conexión de puerta de enlace VPN de sitio a sitio es tooconnect utilizado en sus instalaciones de red tooan red virtual de Azure a través de un túnel VPN de IPsec/IKE (IKEv1 o IKEv2). Este tipo de conexión requiere una VPN dispositivo situado en local que tiene un tooit de dirección asignada de IP pública con orientación externa. Para más información acerca de las puertas de enlace VPN, consulte [Acerca de VPN Gateway](vpn-gateway-about-vpngateways.md).

![Diagrama de la conexión entre locales de VPN Gateway de sitio a sitio](./media/vpn-gateway-howto-site-to-site-classic-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a>Antes de empezar

Compruebe que se ha cumplido hello siguiendo criterios antes de comenzar la configuración:

* Compruebe que desea que toowork en el modelo de implementación clásica de Hola. Si desea que toowork en el modelo de implementación del Administrador de recursos de hello, consulte [crear una conexión de sitio a sitio (Administrador de recursos)](vpn-gateway-howto-site-to-site-resource-manager-portal.md). Cuando sea posible, se recomienda utilizar el modelo de implementación del Administrador de recursos de Hola.
* Asegúrese de que tiene un dispositivo VPN compatible y alguna persona tooconfigure capaz de él. Para más información acerca de los dispositivos VPN compatibles y su configuración, consulte [Acerca de los dispositivos VPN](vpn-gateway-about-vpn-devices.md).
* Compruebe que tiene una dirección IPv4 pública externa para el dispositivo VPN. Esta dirección IP no puede estar detrás de un NAT.
* Si no está familiarizado con intervalos de direcciones IP de hello ubicados en configuración de red local, deberá toocoordinate con alguien que pueda proporcionarle estos detalles para usted. Al crear esta configuración, debe especificar prefijos para intervalo de direcciones IP con hello que Azure enrutará la ubicación de tooyour local. Ninguna de las subredes de saludo de la red local puede enumerar sobre el regazo con subredes de red virtual de Hola que desee tooconnect a.
* Actualmente, PowerShell toospecify requiere una clave compartida hello y crear la conexión de puerta de enlace VPN de Hola. Instalar versión más reciente de Hola de hello cmdlets de PowerShell de administración de servicio de Azure (SM). Para obtener más información, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview). Cuando trabaje con PowerShell para esta configuración, asegúrese de que está ejecutando como administrador. 

### <a name="values"></a>Valores de configuración de ejemplo para este ejercicio

ejemplos de Hello en este artículo utiliza Hola después de valores. Puede usar estos toocreate valores un entorno de prueba, o consulte toothem toobetter comprender los ejemplos de hello en este artículo.

* **Nombre de red virtual:** TestVNet1
* **Espacio de direcciones:** 
  * 10.11.0.0/16
  * 10.12.0.0/16 (opcional para este ejercicio)
* **Subredes:**
  * FrontEnd: 10.11.0.0/24
  * BackEnd: 10.12.0.0/24 (opcional para este ejercicio)
* **GatewaySubnet:** 10.11.255.0/27
* **Grupo de recursos:** TestRG1
* **Ubicación:** este de EE. UU.
* **Servidor DNS:** 10.11.0.3 (opcional para este ejercicio)
* **Nombre del sitio local:** Site2
* **Espacio de direcciones de cliente:** Hola espacio de direcciones que se encuentra en el sitio local.

## <a name="CreatVNet"></a>1. Crear una red virtual

Cuando se crea un toouse de red virtual para una conexión de S2S, deberá toomake seguro de que los espacios de direcciones de Hola que especifique no se superponen con ninguno de los espacios de direcciones de cliente de Hola para sitios locales de Hola que desee tooconnect a. Si tiene subredes superpuestas, la conexión no funcionará correctamente.

* Si ya tiene una red virtual, compruebe que la configuración de hello es compatible con el diseño de la puerta de enlace VPN. Preste especial atención tooany subredes que se pueden superponer con otras redes. 

* Si no tiene una red virtual, créela. Las capturas de pantalla se proporcionan a modo de ejemplo. Ser seguro tooreplace Hola valores por los suyos propios.

### <a name="toocreate-a-virtual-network"></a>toocreate una red virtual

1. Desde un explorador, navegue toohello [portal de Azure](http://portal.azure.com) y, si es necesario, inicie sesión con su cuenta de Azure.
2. Haga clic en **+**. Hola **busque en marketplace hello** , escriba 'Red Virtual'. Busque **red Virtual** de hello devuelve lista y haga clic en hello tooopen **red Virtual** página.

  ![Búsqueda de la página Red virtual](./media/vpn-gateway-howto-site-to-site-classic-portal/newvnetportal700.png)
3. En parte inferior de Hola de página de red Virtual de hello, de hello **seleccionar un modelo de implementación** lista desplegable, seleccione **clásico**y, a continuación, haga clic en **crear**.

  ![Seleccionar modelo de implementación](./media/vpn-gateway-howto-site-to-site-classic-portal/selectmodel.png)
4. En hello **crear network(classic) virtual** página, configure opciones de red virtual de Hola. En esta página, se agrega el primer espacio de direcciones y un intervalo único de direcciones de subred. Cuando termine de crear Hola red virtual, puede volver atrás y agregar espacios de direcciones y subredes adicionales.

  ![Página Crear red virtual](./media/vpn-gateway-howto-site-to-site-classic-portal/createvnet.png "Página Crear red virtual")
5. Compruebe que hello **suscripción** es hello correcto. Puede cambiar las suscripciones mediante Hola de lista desplegable.
6. Haga clic en **Grupo de recursos** y seleccione un grupo de recursos existente, o bien cree uno nuevo escribiendo un nombre. Para más información acerca de los grupos de recursos, visite [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).
7. A continuación, seleccione hello **ubicación** configuración de la red virtual. ubicación de Hello determina dónde se ubicación recursos Hola que implemente toothis red virtual.
8. Si desea que toobe pueda toofind la red virtual fácilmente en el panel de hello, seleccione **toodashboard Pin**. Haga clic en **crear** toocreate la red virtual.

  ![PIN toodashboard](./media/vpn-gateway-howto-site-to-site-classic-portal/pintodashboard150.png "toodashboard de Pin")
9. Después de hacer clic en "Crear", un icono aparece en panel de Hola que refleja el progreso de saludo de la red virtual. Hola de iconos cambia cuando Hola red virtual se está creando.

  ![Icono de creación de red virtual](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png "Creación de red virtual")

Una vez creada la red virtual, vea **creado** aparecen en **estado** en página redes Hola Hola portal de Azure clásico.

## <a name="additionaladdress"></a>2. Incorporación de un espacio de direcciones adicional

Después de crear la red virtual, puede agregar un espacio de direcciones adicional. Agregar espacio de direcciones adicional no es una parte necesaria de una configuración de S2S, pero si necesita varios espacios de direcciones, utilice Hola pasos:

1. Busque las redes virtuales hello en el portal de Hola.
2. En la página de hello para la red virtual, en hello **configuración** sección, haga clic en **espacio de direcciones**.
3. En la página del espacio de dirección de hello, haga clic en **+ agregar** y escriba el espacio de direcciones adicional.

## <a name="dns"></a>3. Especificación de un servidor DNS

La configuración de DNS no es un paso necesario de la configuración de S2S, pero el servidor DNS se necesita para resolver nombres. La especificación de un valor no crea un servidor DNS nuevo. Hello dirección IP del servidor DNS que especifique debe ser un servidor DNS que pueda resolver nombres de Hola para los recursos de saludo a que se está conectando. Para la configuración de ejemplo de Hola, se usa una dirección IP privada. dirección IP de Hello que usamos probablemente no es dirección IP de hello del servidor DNS. Ser seguro toouse sus propios valores.

Después de crear la red virtual, puede agregar la dirección IP de saludo de la resolución de nombres de toohandle de servidor DNS. Abra la configuración de hello para la red virtual, haga clic en servidores DNS y agregar dirección IP de Hola Hola DNS del servidor de que desea toouse para la resolución de nombres.

1. Busque las redes virtuales hello en el portal de Hola.
2. En la página de hello para la red virtual, en hello **configuración** sección, haga clic en **servidores DNS**.
3. Agregue un servidor DNS.
4. toosave su configuración, haga clic en **guardar** al principio de Hola de página de Hola.

## <a name="localsite"></a>4. Configurar el sitio local de Hola

sitio local de Hello suele hacer referencia a ubicación de tooyour local. Contiene dirección IP de Hola de hello VPN dispositivo toowhich que creará una conexión y los intervalos de direcciones IP de Hola que se enrutará a través del dispositivo VPN de toohello de puerta de enlace VPN de Hola.

1. En el portal de hello, navegue toohello red virtual que se desea toocreate una puerta de enlace.
2. En la página de hello para la red virtual, en hello **Introducción** página, en la sección de conexiones de VPN de hello, haga clic en **puerta de enlace** tooopen Hola **conexión VPN nueva** página.

  ![Haga clic en configuración de puerta de enlace de tooconfigure](./media/vpn-gateway-howto-site-to-site-classic-portal/beforegw125.png "haga clic en configuración de puerta de enlace de tooconfigure")
3. En hello **conexión VPN nueva** página, seleccione **sitio a sitio**.
4. Haga clic en **Local del sitio: configurar los valores obligatorios** tooopen hello **sitio Local** página. Configurar opciones de hello y, a continuación, haga clic en **Aceptar** configuración de toosave Hola.
  - **Nombre:** crear un nombre para el sitio local toomake más sencilla para tooidentify.
  - **Dirección IP de puerta de enlace VPN:** es Hola de dirección IP pública del dispositivo VPN de hello para la red local. dispositivo VPN de Hello requiere una dirección IP pública de IPv4. Especifique una dirección IP pública válida para hello toowhich de dispositivo VPN que desea tooconnect. No puede estar detrás de NAT y tiene toobe accesible por Azure. Si desconoce la dirección IP de hello de dispositivo VPN, puede siempre se coloca en un valor de marcador de posición (siempre que se encuentra en formato de Hola de una dirección IP pública válida) y, a continuación, cambiar más adelante.
  - **Espacio de direcciones de cliente:** intervalos de direcciones IP de Hola de lista que desee enrutan toohello red de instalaciones locales a través de esta puerta de enlace. Puede agregar varios intervalos de espacios de direcciones. Asegúrese de que los intervalos de Hola que especifique aquí no se superponen con intervalos de otras redes de a que la red virtual se conecta, o con intervalos de direcciones de saludo de la propia red virtual de Hola.

  ![Sitio local](./media/vpn-gateway-howto-site-to-site-classic-portal/localnetworksite.png "Configuración de sitio local")

## <a name="gatewaysubnet"></a>5. Configurar la subred de puerta de enlace de Hola

Debe crear una subred de puerta de enlace para la puerta de enlace VPN. subred de puerta de enlace de Hello contiene direcciones IP de Hola que utilizan los servicios de puerta de enlace VPN de Hola.

1. En hello **conexión VPN nueva** página, seleccione Hola casilla **crear inmediatamente la puerta de enlace**. aparece en la página Hello 'configuración de puerta de enlace opcionales'. Si no selecciona la casilla de verificación de hello, no verá subred de puerta de enlace de hello página tooconfigure Hola.

  ![Configuración de puerta de enlace: subred, tamaño, tipo de enrutamiento](./media/vpn-gateway-howto-site-to-site-classic-portal/optional.png "Configuración de puerta de enlace: subred, tamaño, tipo de enrutamiento")
2. Hola tooopen **configuración de puerta de enlace** página, haga clic en **configuración opcional de la puerta de enlace - subred, tamaño y tipo de enrutamiento**.
3. En hello **configuración de puerta de enlace** página, haga clic en **subred - configurar los valores obligatorios** tooopen hello **Agregar subred** página.

  ![Configuración de puerta de enlace: subred de puerta de enlace](./media/vpn-gateway-howto-site-to-site-classic-portal/subnetrequired.png "Configuración de puerta de enlace: subred de puerta de enlace")
4. En hello **Agregar subred** página, agregue una subred de puerta de enlace de Hola. tamaño de Hola de subred de puerta de enlace de Hola que especifique depende en configuración de puerta de enlace VPN de Hola que desea toocreate. Aunque es posible toocreate una subred de puerta de enlace tan pequeña como /29, se recomienda que use /27 o /28. Esto crea una subred mayor que incluye más direcciones. Mediante una subred de puerta de enlace mayor permite suficiente IP direcciones tooaccommodate futuras configuraciones posibles.

  ![Agregar subred de puerta de enlace](./media/vpn-gateway-howto-site-to-site-classic-portal/addgwsubnet.png "Agregar subred de puerta de enlace")

## <a name="sku"></a>6. Especificar Hola SKU y el tipo VPN

1. Puerta de enlace de hello seleccione **tamaño**. Se trata de puerta de enlace de hello SKU que usar toocreate la puerta de enlace de red virtual. En el portal de hello, Hola 'SKU predeterminado' = **básica**. Puertas de enlace VPN clásicos utilizar Hola anterior (heredado) puerta de enlace de SKU. Para obtener más información acerca de la puerta de enlace heredado de hello SKU, consulte [trabajar con la puerta de enlace de red virtual SKU (SKU antiguas)](vpn-gateway-about-skus-legacy.md).

  ![Seleccionar tipo de VPN y SKU](./media/vpn-gateway-howto-site-to-site-classic-portal/sku.png "Seleccionar tipo de VPN y SKU")
2. Seleccione hello **tipo de enrutamiento** para la puerta de enlace. Se trata también conocido como de tipo de VPN de Hola. Es del tipo de puerta de enlace correcto de hello tooselect importante porque no se puede convertir puerta de enlace de Hola de tooanother de un tipo. El dispositivo VPN debe ser compatible con el tipo de enrutamiento de Hola que seleccione. Para más información sobre el tipo de VPN, consulte [Acerca de la configuración de VPN Gateway](vpn-gateway-about-vpn-gateway-settings.md#vpntype). Es posible que vea los artículos que hace referencia too'RouteBased' y 'PolicyBased' VPN tipos. ' Dynamic 'corresponde too'RouteBased', y corresponde 'Static' a 'PolicyBased'.
3. Haga clic en **Aceptar** configuración de toosave Hola.
4. En hello **conexión VPN nueva** página, haga clic en **Aceptar** final Hola de hello página toobegin crear la puerta de enlace de red virtual. Función hello SKU que seleccione, puede tardar hasta too45 minutos toocreate una puerta de enlace de red virtual.

## <a name="vpndevice"></a>7. Configurar el dispositivo VPN

Red local de las conexiones de sitio a sitio tooan requieren un dispositivo VPN. En este paso, se configura el dispositivo VPN. Al configurar el dispositivo VPN, necesita Hola siguiente:

- Una clave compartida. Esto es Hola mismo compartido clave que se especifique al crear la conexión VPN de sitio a sitio. En estos ejemplos se utiliza una clave compartida básica. Se recomienda que generar un toouse clave más compleja.
- Hola dirección IP pública de la puerta de enlace de red virtual. Puede ver la dirección IP pública hello mediante Hola portal de Azure, PowerShell o CLI.

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a>8. Crear conexiones de Hola
En este paso, establecer clave compartida de Hola y crear la conexión de Hola. clave de Hello establece debe estar Hola misma clave que se utilizó en la configuración del dispositivo VPN.

> [!NOTE]
> Actualmente, este paso no está disponible en hello portal de Azure. Debe usar la versión de Service Management (SM) Hola de hello cmdlets de PowerShell de Azure.
>

### <a name="step-1-connect-tooyour-azure-account"></a>Paso 1. Conectar tooyour cuenta de Azure

1. Abra la consola de PowerShell con derechos elevados y conectar con tooyour cuenta. Usar hello después toohelp de ejemplo que se conecta:

  ```powershell
  Add-AzureAccount
  ```
2. Compruebe las suscripciones de hello para la cuenta de hello.

  ```powershell
  Get-AzureSubscription
  ```
3. Si tiene más de una suscripción, seleccione Hola suscripción que desea toouse.

  ```powershell
  Select-AzureSubscription -SubscriptionId "Replace_with_your_subscription_ID"
  ```

### <a name="step-2-set-hello-shared-key-and-create-hello-connection"></a>Paso 2: Establecer clave compartida de Hola y crear la conexión de Hola

Cuando se trabaja con modelos de implementación clásica de PowerShell y hello, a veces Hola nombres de recursos en el portal de hello no son Hola nombres Hola Azure espera toosee cuando se usa PowerShell. Hello pasos siguientes ayuda a exportar Hola red archivo tooobtain Hola exacta valores de configuración para los nombres de Hola.

1. Cree un directorio en el equipo y, a continuación, exportar el directorio de toohello de archivo de configuración de red de Hola. En este ejemplo, el archivo de configuración de red de hello es tooC:\AzureNet exportado.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. Abra el archivo de configuración de red de hello con un editor xml y comprobar los valores de hello 'Nombre de LocalNetworkSite' y 'Nombre de VirtualNetworkSite'. Modificar valores de hello de tooreflect de ejemplo de Hola que necesita. Al especificar un nombre que contiene espacios, use comillas simples en el valor de Hola.

3. Establecer clave compartida de Hola y crear la conexión de Hola. Hola '-SharedKey' es un valor que se generan y se especifica. En el ejemplo de Hola, hemos usado "abc123", pero puede generar (y debe) usar algo más complejo. Hola importante que es ese valor de Hola que especifique aquí debe ser Hola que mismo valor que especificó al configurar el dispositivo VPN.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group TestRG1 TestVNet1' `
  -LocalNetworkSiteName 'D1BFC9CB_Site2' -SharedKey abc123
  ```
Cuando se crean conexiones de hello, resultado de hello es: **estado: correcto**.

## <a name="verify"></a>9. Comprobación de la conexión

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

Si tiene problemas para conectarse, vea hello **solucionar** sección de la tabla de contenido en el panel izquierdo de Hola Hola.

## <a name="reset"></a>¿Cómo tooreset una puerta de enlace VPN

Restablecer una puerta de enlace de VPN de Azure es útil si se pierde la conectividad VPN entre locales en uno o varios túneles VPN de sitio a sitio. En esta situación, los dispositivos VPN local son todo funciona correctamente, pero son tooestablish imposibilidad de túneles de IPsec con puertas de enlace de VPN de Azure de Hola. Para conocer los pasos, consulte [Restablecimiento de una puerta de enlace de VPN](vpn-gateway-resetgw-classic.md).

## <a name="changesku"></a>¿Cómo toochange una SKU de puerta de enlace

Para los pasos de hello toochange una SKU de puerta de enlace, vea [cambiar el tamaño de una puerta de enlace SKU](vpn-gateway-about-SKUS-legacy.md).

## <a name="next-steps"></a>Pasos siguientes

* Una vez completada la conexión, puede agregar redes virtuales de máquinas virtuales tooyour. Consulte [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) para más información.
* Para más información acerca de la tunelización forzada, consulte la [información acerca de la tunelización forzada](vpn-gateway-about-forced-tunneling.md).