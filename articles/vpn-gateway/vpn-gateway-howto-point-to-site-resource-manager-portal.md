---
title: "Conectar una red virtual de tooa de equipo mediante la autenticación de certificado y de Point-to-Site: Portal de Azure | Documentos de Microsoft"
description: "Conectarse de forma segura una red Virtual de Azure tooyour de equipo mediante la creación de una conexión de puerta de enlace de Point-to-Site VPN mediante la autenticación de certificado. En este artículo se aplica el modelo de implementación del Administrador de recursos de toohello y usa Hola portal de Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a15ad327-e236-461f-a18e-6dbedbf74943
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: 1419d6b4c160140b62d656b25bd02f6af7fd6655
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-azure-portal"></a>Configurar una tooa de conexión de punto a sitio red virtual mediante la autenticación de certificado: portal de Azure

Este artículo muestra cómo toocreate una red virtual con una conexión de punto a sitio en el modelo de implementación de administrador de recursos de hello utilizando Hola portal de Azure. Esta configuración utiliza Hola de tooauthenticate certificados conecta el cliente. También puede crear esta configuración con una herramienta de implementación diferentes o un modelo de implementación seleccionando una opción diferente de hello lista siguiente:

> [!div class="op_single_selector"]
> * [Portal de Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Portal de Azure clásico](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

Una puerta de enlace VPN de punto a sitio (P2S) le permite crear una red virtual de tooyour de conexión segura desde un equipo cliente individual. Las conexiones de VPN de sitio a punto son útiles cuando se desea tooconnect tooyour red virtual desde una ubicación remota, como cuando trabajan a distancia desde casa o una conferencia. Una VPN P2S también es un toouse solución útil en lugar de una VPN de sitio a sitio cuando hay solo unos clientes que necesitan tooconnect tooa red virtual. 

Usa P2S Hola Secure Socket de protocolo de túnel (SSTP), que es un protocolo VPN basada en SSL. Se establece una conexión VPN P2S, empiece por equipo de cliente de Hola.

![Diagrama de punto a sitio](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/point-to-site-connection-diagram.png)

Las conexiones de autenticación de certificado de punto a sitio requieren siguientes de hello:

* Una puerta de enlace de VPN RouteBased.
* Hola clave pública (archivo .cer) para un certificado raíz, que es cargado tooAzure. Una vez cargado el certificado de hello, se considera un certificado de confianza y se utiliza para la autenticación.
* Un certificado de cliente que se genera a partir de certificado de raíz de Hola e instalado en cada equipo cliente que se conectará toohello red virtual. Este certificado se usa para la autenticación de cliente.
* Un paquete de configuración de cliente de VPN. paquete de configuración de cliente VPN de Hello contiene información necesaria de Hola para hello cliente tooconnect toohello red virtual. paquete de Hello configura el cliente VPN existente hello es nativo toohello sistema operativo Windows. Cada cliente que se conecta debe configurarse mediante el paquete de configuración de Hola.

Las conexiones de punto a sitio no requieren un dispositivo VPN ni una dirección IP de acceso público local. Hola conexión VPN se crea a través de SSTP (Protocolo de túnel de sockets de seguros). En el lado del servidor hello, se admiten las versiones 1.0, 1.1 y 1.2 de SSTP. cliente de Hello decide qué toouse de versión. Para Windows 8.1 y versiones posteriores, SSTP usa 1.2 de forma predeterminada.

Para obtener más información acerca de las conexiones punto a sitio, vea hello [Point-to-Site preguntas más frecuentes sobre](#faq) final Hola de este artículo.

#### <a name="example"></a>Valores del ejemplo

Puede usar hello después valores toocreate un entorno de prueba, o consultar valores toothese toobetter comprender los ejemplos de hello en este artículo:

* **Nombre de la red virtual:** VNet1
* **Espacio de direcciones:** 192.168.0.0/16<br>En este ejemplo, se utiliza solo un espacio de direcciones. Puede tener más de un espacio de direcciones para la red virtual.
* **Nombre de subred:** FrontEnd
* **Intervalo de direcciones de subred:** 192.168.1.0/24
* **Suscripción:** si tiene más de una suscripción, compruebe que está usando Hola correcto.
* **Grupo de recursos:** TestRG
* **Ubicación:** este de EE. UU.
* **GatewaySubnet:** 192.168.200.0/24<br>
* **Servidor DNS:** (opcional) dirección IP del servidor DNS de Hola que quiere toouse de resolución de nombres.
* **Nombre de la puerta de enlace de red virtual:** VNet1GW
* **Tipo de puerta de enlace:** VPN
* **Tipo de VPN:** basada en rutas
* **Dirección IP pública:** VNet1GWpip
* **Tipo de conexión:** de punto a sitio
* **Grupo de direcciones de clientes:** 172.16.201.0/24<br>Los clientes VPN que se conectan toohello red virtual con esta conexión de punto a sitio reciben una dirección IP del grupo de direcciones de cliente de Hola.

## <a name="createvnet"></a>1. Crear una red virtual

Antes de empezar, compruebe que tiene una suscripción a Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) o registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial).

[!INCLUDE [Basic Point-to-Site VNet](../../includes/vpn-gateway-basic-p2s-vnet-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>2. Adición de una subred de puerta de enlace

Antes de conectar la puerta de enlace de red virtual tooa, primero debe subred de puerta de enlace de toocreate Hola Hola toowhich de red virtual se desea tooconnect. Servicios de puerta de enlace de Hello utilizan direcciones IP de hello especificadas en la subred de puerta de enlace de Hola. Si es posible, cree una subred de puerta de enlace con un bloque CIDR de /28 o /27 tooprovide suficiente IP direcciones tooaccommodate requisitos de configuración futura adicional.

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-p2s-rm-portal-include.md)]

## <a name="dns"></a>3. Especificación de un servidor DNS (opcional)

Después de crear la red virtual, puede agregar la dirección IP de saludo de la resolución de nombres de toohandle de servidor DNS. servidor DNS de Hello es opcional para esta configuración, pero es necesario si desea que la resolución de nombres. La especificación de un valor no crea un servidor DNS nuevo. Hello dirección IP del servidor DNS que especifique debe ser un servidor DNS que pueda resolver nombres de Hola para los recursos de saludo a que se está conectando. En este ejemplo, se usa una dirección IP privada, pero es probable que esto no es Hola dirección IP del servidor DNS. Ser seguro toouse sus propios valores.

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="creategw"></a>4. Creación de una puerta de enlace de red virtual

[!INCLUDE [create-gateway](../../includes/vpn-gateway-add-gw-p2s-rm-portal-include.md)]

## <a name="generatecert"></a>5. Generación de certificados

Los clientes de Azure tooauthenticate tooa red virtual a través de una conexión VPN de sitio a punto de conexión se usan certificados. Una vez que obtenga un certificado raíz, se [cargar](#uploadfile) Hola tooAzure de información de clave pública. certificado de raíz de Hello, a continuación, se considera "confianza' Azure para la conexión a través de la red virtual de P2S toohello. También generar certificados de cliente de certificado de raíz de confianza de hello y, a continuación, vuelva a instalarlos en cada equipo cliente. certificado de cliente de Hello es cliente de hello tooauthenticate usado cuando inicia una red virtual toohello de conexión. 

### <a name="getcer"></a>1. Obtener el archivo .cer de hello para el certificado de raíz de Hola

[!INCLUDE [root-certificate](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <a name="generateclientcert"></a>2. Generación de un certificado de cliente

[!INCLUDE [generate-client-cert](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="addresspool"></a>6. Agregar grupo de direcciones de cliente hello

grupo de direcciones de cliente Hello es un intervalo de direcciones IP privadas que se especifican. los clientes de Hola que se conectan a través de una VPN de punto a sitio reciben una dirección IP de este intervalo. Usar un intervalo de direcciones IP privadas que no se superponen con ubicación local de Hola que se conectan desde u Hola red virtual que desea tooconnect a.

1. Una vez creada la puerta de enlace de red virtual de hello, navegue toohello **configuración** sección de página de puerta de enlace de red virtual de Hola. Hola **configuración** sección, haga clic en **configuraciónPoint-to-site** tooopen hello **-a-sitio-configuración del punto de** página.

  ![Página de punto a sitio](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/gatewayblade.png)
2. En hello **-a-sitio-configuración del punto de** página, puede eliminar el intervalo de relleno automático de Hola y luego agregar Hola privada intervalo de direcciones IP que desea toouse. Haga clic en **guardar** toovalidate y guardar la configuración de Hola.

  ![Grupo de direcciones de clientes](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/ipaddresspool.png)

## <a name="uploadfile"></a>7. Cargar datos de certificado público del certificado de raíz de Hola

Una vez creada la puerta de enlace de hello, cargar información de clave pública de Hola para tooAzure de certificado de raíz de Hola. Una vez que se cargan los datos de certificado público de hello, Azure puede usar a los clientes de tooauthenticate que han instalado un certificado de cliente generado a partir de certificado de raíz de confianza de Hola. Puede cargar el total de tooa de seguridad de certificados raíz de confianza adicionales de 20.

1. Los certificados se agregan en hello **configuraciónPoint-to-site** página Hola **certificado raíz** sección.  
2. Asegúrese de que exporta el certificado de raíz de hello como archivo X.509 (.cer) codificado en Base 64. Se necesita certificado de Hola de tooexport en este formato para que pueda abrir certificado Hola con el editor de texto.
3. Abra Hola certificado con un editor de texto, como el Bloc de notas. Cuando se copian datos de certificado de hello, asegúrese de que copia texto hello como una línea continua sin retornos de carro o avances de línea. Deberá toomodify la vista mediante too'Show de editor de texto hello símbolos/mostrar toosee Hola de carro todos los caracteres devuelve y saltos de línea. Copiar solo Hola pasos de la sección como una línea continua:

  ![Datos del certificado](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/copycert.png)
4. Pegar datos del certificado de hello en hello **datos del certificado público** campo. **Nombre** Hola certificado y, a continuación, haga clic en **guardar**. Puede agregar los certificados raíz de too20 de confianza.

  ![Carga del certificado](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/rootcertupload.png)

## <a name="clientconfig"></a>8. Generar e instalar el paquete de configuración de cliente VPN de Hola

tooconnect tooa red virtual con una VPN de sitio a punto, cada cliente debe instalar un paquete de configuración de cliente que se configura el cliente VPN nativo que Hola con los valores de hello y archivos de red virtual de toohello tooconnect necesarios. paquete de configuración de cliente VPN de Hello configura el cliente de VPN de Windows nativo hello, pero no instala un cliente VPN de nuevo o diferente.

Puede usar Hola misma configuración de cliente VPN del paquete en cada equipo cliente, como versión de Hola coincida con la arquitectura de hello para el cliente de Hola. Para hello obtener lista de sistemas operativos cliente que son compatibles, vea hello [conexionesPoint-to-Site preguntas más frecuentes sobre](#faq) final Hola de este artículo.

### <a name="step-1---generate-and-download-hello-client-configuration-package"></a>Paso 1: generar y descargar el paquete de configuración de cliente de Hola

1. En hello **configuraciónPoint-to-site** página, haga clic en **cliente VPN descargar** tooopen hello **cliente VPN descargar** página. Tarda un minuto o dos para toogenerate de paquetes de saludo.

  ![Descarga del cliente de VPN 1](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/downloadvpnclient1.png)
2. Seleccione el paquete correcto de Hola para su cliente y, a continuación, haga clic en **descargar**. Guarde el archivo de paquete de configuración de Hola. Instale el paquete de configuración de cliente VPN de hello en cada equipo cliente que se conecta la red virtual toohello.

  ![Descarga del cliente de VPN 2](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/vpnclient.png)

### <a name="step-2---install-hello-client-configuration-package"></a>Paso 2: paquete de configuración de cliente de instalación Hola

1. Archivo de configuración de copia hello localmente un toohello equipo que desea que la red virtual de tooconnect tooyour. 
2. Haga doble clic en el paquete de Hola Hola .exe archivos tooinstall en el equipo cliente de Hola. Dado que creó el paquete de configuración de hello, no está firmado y verá una advertencia. Si aparece un menú emergente de Windows SmartScreen, haga clic en **obtener más información** (en hello izquierda), a continuación, **ejecutar de todos modos** paquete de hello tooinstall.
3. Instale el paquete de hello en el equipo cliente de Hola. Si aparece un menú emergente de Windows SmartScreen, haga clic en **obtener más información** (en hello izquierda), a continuación, **ejecutar de todos modos** paquete de hello tooinstall.
4. En el equipo de cliente hello, vaya demasiado**configuración de red** y haga clic en **VPN**. Hola conexión VPN muestra nombre Hola de red virtual de Hola que se conecta a.

## <a name="installclientcert"></a>9. Instalación de un certificado de cliente exportado

Si desea toocreate una P2S conexión desde un equipo cliente que no sea de Hola que utiliza certificados de cliente hello toogenerate, deberá tooinstall un certificado de cliente. Al instalar un certificado de cliente, necesita contraseña Hola que se creó cuando se exporta el certificado de cliente de Hola. Normalmente, es simplemente cuestión de doble clic en el certificado de hello e instalarla.

Asegúrese de que se exportó el certificado de cliente de Hola como un .pfx junto con la cadena de certificados completa de hello (que es el valor predeterminado de hello). En caso contrario, no está presente en el equipo de cliente hello información del certificado de raíz de Hola y cliente hello no será capaz de tooauthenticate correctamente. Para más información, consulte [Instalación de un certificado de cliente exportado](vpn-gateway-certificates-point-to-site.md#install).

## <a name="connect"></a>10. Conectar tooAzure

1. tooconnect tooyour de red virtual, en el equipo de cliente hello, navegar por las conexiones de tooVPN y encontrar la conexión de VPN de Hola que ha creado. Se denomina hello mismo nombre como la red virtual. Haga clic en **Conectar**. Puede aparecer un mensaje emergente que hace referencia el certificado de hello toousing. Haga clic en **continuar** toouse privilegios elevados.

2. En hello **conexión** página de estado, haga clic en **conectar** conexión de hello toostart. Si ve un **Seleccionar certificado** pantalla, compruebe que Hola cliente certificado que se muestra es Hola uno que desea toouse tooconnect. Si no es así, utilice certificado correcto de hello flecha de lista desplegable tooselect hello y, a continuación, haga clic en **Aceptar**.

  ![TooAzure conecta el cliente VPN](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/clientconnect.png)
3. Se ha establecido la conexión.

  ![Conexión establecida](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>Solución de problemas de conexiones P2S

[!INCLUDE [verifies client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <a name="verify"></a>11. Comprobación de la conexión

1. tooverify que la conexión VPN esté activa, abra un símbolo del sistema con privilegios elevados y ejecute *ipconfig/all*.
2. Ver los resultados de Hola. Tenga en cuenta que la dirección IP de hello recibió es una de las direcciones de hello en el grupo de direcciones de cliente VPN de hello Point-to-Site que especificó en la configuración. resultados de Hello son similares de toothis de ejemplo:

  ```
  PPP adapter VNet1:
      Connection-specific DNS Suffix .:
      Description.....................: VNet1
      Physical Address................:
      DHCP Enabled....................: No
      Autoconfiguration Enabled.......: Yes
      IPv4 Address....................: 172.16.201.3(Preferred)
      Subnet Mask.....................: 255.255.255.255
      Default Gateway.................:
      NetBIOS over Tcpip..............: Enabled
  ```

## <a name="connectVM"></a>Conectar máquina virtual de tooa

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <a name="add"></a>Incorporación o eliminación de certificados raíz de confianza

Puede agregar y quitar certificados raíz de confianza de Azure. Cuando se quita un certificado raíz, los clientes que tienen un certificado generado a partir de esa raíz no será capaz de tooauthenticate y, por tanto, no será capaz de tooconnect. Si desea que un cliente tooauthenticate y conectarse, debe tooinstall genera un nuevo certificado de cliente de un certificado raíz de confianza tooAzure (cargado).

### <a name="tooadd-a-trusted-root-certificate"></a>tooadd un certificado raíz de confianza

Puede sumar too20 confianza raíz certificado .cer archivos tooAzure. Para obtener instrucciones, consulte la sección de hello [cargar un certificado raíz de confianza](#uploadfile) en este artículo.

### <a name="tooremove-a-trusted-root-certificate"></a>tooremove un certificado raíz de confianza

1. tooremove un certificado raíz de confianza, navegue toohello **configuraciónPoint-to-site** página de la puerta de enlace de red virtual.
2. Hola **certificado raíz** sección de página de hello, busque el certificado de Hola que desea tooremove.
3. Haga clic en siguiente toohello certificado de puntos suspensivos de hello y, a continuación, haga clic en "Eliminar".

## <a name="revokeclient"></a>Revocación de un certificado de cliente

Puede revocar certificados de cliente. podrá tooselectively lista de revocación de certificados de Hello denegar conectividad de punto a sitio basada en certificados de cliente individuales. Esto difiere de la forma en que se quita un certificado raíz de confianza. Si quita un .cer del certificado raíz de confianza de Azure, revoca el acceso de Hola para todos los certificados de cliente generado y firmado por certificado de raíz revocados Hola. Revocar un certificado de cliente, en lugar de certificado de raíz de hello, permite Hola otros certificados que se generaron desde el certificado de raíz de hello toocontinue toobe utilizado para la autenticación.

una práctica habitual Hello es toouse Hola certificado toomanage acceso a la raíz en los niveles de equipo u organización, durante el uso de certificados de cliente revocados para el control de acceso específica para los usuarios individuales.

### <a name="toorevoke-a-client-certificate"></a>toorevoke un certificado de cliente

Puede revocar un certificado de cliente mediante la adición de la lista de revocación de toohello Hola huella digital.

1. Recuperar la huella digital del certificado de cliente de Hola. Para obtener más información, consulte [cómo tooretrieve Hola huella digital de un certificado](https://msdn.microsoft.com/library/ms734695.aspx).
2. Copiar información hello tooa, editor de texto y quite todos los espacios para que sea una sola cadena continua.
3. Navegar por la puerta de enlace de red virtual de toohello **-a-sitio-configuración del punto de** página. Se trata de hello sintonía que usó demasiado[cargar un certificado raíz de confianza](#uploadfile).
4. Hola **certificados revocados** sección, escriba un nombre descriptivo para el certificado de hello (no tiene certificado de hello toobe CN).
5. Copie y pegue Hola huella digital cadena toohello **huella digital** campo.
6. huella digital de Hello valida y se agrega automáticamente la lista de revocación de toohello. Aparece un mensaje en la pantalla de bienvenida que Hola lista se está actualizando. 
7. Una vez finalizada la actualización, certificado de hello ya no puede ser tooconnect usado. Los clientes que intentan tooconnect con este certificado, aparece un mensaje que indica que dicho certificado Hola ya no es válido.

## <a name="faq"></a>Preguntas más frecuentes sobre la conexión de punto a sitio

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Pasos siguientes
Una vez completada la conexión, puede agregar redes virtuales de máquinas virtuales tooyour. Consulte [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) para más información. toounderstand más información acerca de las redes y máquinas virtuales, consulte [información general de red de Azure y VM de Linux](../virtual-machines/linux/azure-vm-network-overview.md).
