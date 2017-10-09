---
title: "Conectar una red virtual de tooa de equipo mediante la autenticación de certificado y de Point-to-Site: clásico de Portal de Azure | Documentos de Microsoft"
description: "Conectarse de forma segura tooyour clásico red Virtual de Azure mediante la creación de una conexión de puerta de enlace VPN de sitio a punto mediante Hola portal de Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 65e14579-86cf-4d29-a6ac-547ccbd743bd
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 9b53ba43ee4dfb61defeec458905fb1f1b18c3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-classic-azure-portal"></a>Configurar una tooa de conexión de punto a sitio red virtual mediante la autenticación de certificado (clásico): portal de Azure

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

Este artículo muestra cómo toocreate una red virtual con una conexión de punto a sitio en el modelo de implementación clásica de hello utilizando Hola portal de Azure. Esta configuración utiliza Hola de tooauthenticate certificados conecta el cliente. También puede crear esta configuración con una herramienta de implementación diferentes o un modelo de implementación seleccionando una opción diferente de hello lista siguiente:

> [!div class="op_single_selector"]
> * [Portal de Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Portal de Azure clásico](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>

Una puerta de enlace VPN de punto a sitio (P2S) le permite crear una red virtual de tooyour de conexión segura desde un equipo cliente individual. Las conexiones de VPN de sitio a punto son útiles cuando se desea tooconnect tooyour red virtual desde una ubicación remota, como cuando trabajan a distancia desde casa o una conferencia. Una VPN P2S también es un toouse solución útil en lugar de una VPN de sitio a sitio cuando hay solo unos clientes que necesitan tooconnect tooa red virtual. 

Usa P2S Hola Secure Socket de protocolo de túnel (SSTP), que es un protocolo VPN basada en SSL. Se establece una conexión VPN P2S, empiece por equipo de cliente de Hola.


![Diagrama de punto a sitio](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/point-to-site-connection-diagram.png)


Las conexiones de autenticación de certificado de punto a sitio requieren siguientes de hello:

* Una puerta de enlace VPN dinámica.
* Hola clave pública (archivo .cer) para un certificado raíz, que es cargado tooAzure. Esto se considera un certificado de confianza y se usa para la autenticación.
* Un certificado de cliente generados a partir de certificado de raíz de Hola e instalado en cada equipo cliente que se conectará. Este certificado se usa para la autenticación de cliente.
* Se debe generar un paquete de configuración de cliente de VPN e instalarlo en todos los equipos cliente que se conectan. paquete de configuración de cliente de Hello configura a Hola cliente de VPN nativo que ya está en el sistema operativo de hello con hello información necesaria tooconnect toohello red virtual.

Las conexiones de punto a sitio no requieren un dispositivo VPN ni una dirección IP de acceso público local. Hola conexión VPN se crea a través de SSTP (Protocolo de túnel de sockets de seguros). En el lado del servidor hello, se admiten las versiones 1.0, 1.1 y 1.2 de SSTP. cliente de Hello decide qué toouse de versión. Para Windows 8.1 y versiones posteriores, SSTP usa 1.2 de forma predeterminada. 

Para obtener más información acerca de las conexiones punto a sitio, vea hello [Point-to-Site preguntas más frecuentes sobre](#faq) final Hola de este artículo.

### <a name="example-settings"></a>Configuración de ejemplo

Puede usar hello después valores toocreate un entorno de prueba, o consultar valores toothese toobetter comprender los ejemplos de hello en este artículo:

* **Nombre: VNet1**
* **Espacio de direcciones: 192.168.0.0/16**<br>En este ejemplo, se utiliza solo un espacio de direcciones. Puede tener más de un espacio de direcciones para la red virtual.
* **Nombre de subred: FrontEnd**
* **Intervalo de direcciones de subred: 192.168.1.0/24**
* **Suscripción:** si tiene más de una suscripción, compruebe que está usando Hola correcto.
* **Grupo de recursos: TestRG**
* **Ubicación: este de EE. UU.**
* **Tipo de conexión: de punto a sitio**
* **Espacio de direcciones de clientes: 172.16.201.0/24**. Los clientes VPN que se conectan toohello con esta conexión de punto a sitio de red virtual recibirá una dirección IP de Hola grupo especificado.
* **GatewaySubnet: 192.168.200.0/24**. subred de puerta de enlace de Hello debe utilizar Hola nombre 'GatewaySubnet'.
* **Tamaño:** puerta de enlace de hello seleccione SKU que desea toouse.
* **Tipo de enrutamiento: dinámico**

## <a name="vnetvpn"></a>1. Crear una red virtual y una puerta de enlace de VPN

Antes de empezar, compruebe que tiene una suscripción a Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) o registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial).

### <a name="createvnet"></a>Paso 1: Creación de una red virtual

Si no tiene una red virtual, créela. Las capturas de pantalla se proporcionan a modo de ejemplo. Ser seguro tooreplace Hola valores por los suyos propios. toocreate una red virtual mediante el uso de Hola portal de Azure, Hola uso pasos:

1. Desde un explorador, navegue toohello [portal de Azure](http://portal.azure.com) y, si es necesario, inicie sesión con su cuenta de Azure.
2. Haga clic en **Nuevo**. Hola **busque en marketplace hello** , escriba 'Red Virtual'. Busque **red Virtual** de hello devuelve lista y haga clic en hello tooopen **red Virtual** página.

  ![Búsqueda de la página Red virtual](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvnetportal700.png)
3. En parte inferior de Hola de página de red Virtual de hello, de hello **seleccionar un modelo de implementación** seleccione **clásico**y, a continuación, haga clic en **crear**.

  ![Seleccionar modelo de implementación](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/selectmodel.png)
4. En hello **crear red virtual** página, configure opciones de red virtual de Hola. En esta página, se agrega el primer espacio de direcciones y un intervalo único de direcciones de subred. Cuando termine de crear Hola red virtual, puede volver atrás y agregar espacios de direcciones y subredes adicionales.

  ![Crear la página de la red virtual](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/vnet125.png)
5. Compruebe que hello **suscripción** es hello correcto. Puede cambiar las suscripciones mediante Hola de lista desplegable.
6. Haga clic en **Grupo de recursos** y seleccione un grupo de recursos existente, o bien cree uno nuevo escribiendo un nombre para el nuevo grupo. Si está creando un nuevo grupo de recursos, grupo de recursos de nombre hello según tooyour había planeada valores de configuración. Para más información acerca de los grupos de recursos, visite [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).
7. A continuación, seleccione hello **ubicación** configuración de la red virtual. ubicación de Hello determina dónde se ubicación recursos Hola que implemente toothis red virtual.
8. Seleccione **Pin toodashboard** si desea toobe pueda toofind la red virtual fácilmente en el panel de hello y, a continuación, haga clic en **crear**.

  ![Toodashboard de PIN](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/pintodashboard150.png)
9. Después de hacer clic en crear, un icono aparece en el panel que reflejará el progreso de saludo de la red virtual. Hola de iconos cambia cuando Hola red virtual se está creando.

  ![Icono de Crear red virtual](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png)
10. Una vez creada la red virtual, vea **creado** aparecen en **estado** en página redes Hola Hola portal de Azure clásico.
11. Agregue un servidor DNS (opcional). Después de crear la red virtual, puede agregar la dirección IP de Hola de un servidor DNS para la resolución de nombres. Hola dirección IP del servidor DNS que especifique debe ser la dirección de Hola de un servidor DNS que pueda resolver nombres de Hola para los recursos de hello en la red virtual.<br>tooadd un servidor DNS, abra la configuración de hello para la red virtual, haga clic en servidores DNS y agregar dirección IP de Hola Hola DNS del servidor de que desea toouse.

### <a name="gateway"></a>Parte 2: Creación de una subred de puerta de enlace y una puerta de enlace de enrutamiento dinámico

En este paso se crea una subred de puerta de enlace y una puerta de enlace de enrutamiento dinámico. En el portal de Azure para el modelo de implementación clásica de Hola Hola, creación de subred de puerta de enlace de Hola y puerta de enlace de hello puede realizarse a través Hola mismo páginas de configuración.

1. En el portal de hello, navegue toohello red virtual que se desea toocreate una puerta de enlace.
2. En la página de hello para la red virtual, en hello **Introducción** página, en la sección de conexiones de VPN de hello, haga clic en **puerta de enlace**.

  ![Haga clic en toocreate una puerta de enlace](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/beforegw125.png)
3. En hello **conexión VPN nueva** página, seleccione **Point-to-site**.

  ![Tipo de conexión de punto a sitio](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvpnconnect.png)
4. Para **espacio de direcciones de cliente**, agregar el intervalo de direcciones IP de Hola. Se trata de un intervalo de Hola desde el cual los clientes VPN de Hola reciban una dirección IP al conectarse. Usar un intervalo de direcciones IP privadas que no se superponen con ubicación local de Hola que se conecten desde o con hello red virtual que desea tooconnect a. Puede eliminar el intervalo de relleno automático de Hola y luego agregar Hola privada intervalo de direcciones IP que desea toouse.

  ![Espacio de direcciones del cliente](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientaddress.png)
5. Seleccione hello **crear inmediatamente la puerta de enlace** casilla de verificación.

  ![Crear puerta de enlace inmediatamente](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/creategwimm.png)
6. Haga clic en **configuración opcional de la puerta de enlace** tooopen hello **configuración de puerta de enlace** página.

  ![Haga clic en Configuración de puerta de enlace opcional](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/optsubnet125.png)
7. Haga clic en **subred configurar los valores obligatorios** tooadd hello **subred de puerta de enlace**. Aunque es posible toocreate una subred de puerta de enlace tan pequeña como /29, le recomendamos que cree una subred mayor que incluye direcciones más si se selecciona al menos /28 o /27. Esto le permitirá suficientes direcciones tooaccommodate posibles configuraciones adicionales que puede querer en hello futuras. Cuando se trabaja con subredes de puerta de enlace, evite asociar una subred de puerta de enlace de seguridad (NSG) del grupo toohello. Asociar una subred de toothis del grupo de seguridad de red puede provocar la toostop de puerta de enlace VPN que funciona según lo previsto.

  ![Agregue GatewaySubnet](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsubnet125.png)
8. Puerta de enlace de hello seleccione **tamaño**. tamaño de Hello es la puerta de enlace Hola SKU para la puerta de enlace de red virtual. En el portal de hello, hello predeterminado SKU es **básica**. Para más información acerca de las SKU de puerta de enlace, consulte [Acerca de la configuración de VPN Gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

  ![Tamaño de puerta de enlace](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsize125.png)
9. Seleccione hello **tipo de enrutamiento** para la puerta de enlace. Las configuraciones P2S requieren un tipo de enrutamiento **dinámico**. Haga clic en **Aceptar** cuando haya terminado de configurar la página.

  ![Configurar tipo de enrutamiento](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/routingtype125.png)
10. En hello **conexión VPN nueva** página, haga clic en **Aceptar** final Hola de hello página toobegin crear la puerta de enlace de red virtual. Una puerta de enlace VPN puede tardar hasta too45 toocomplete de minutos, dependiendo de la sku de puerta de enlace de Hola que seleccione.

## <a name="generatecerts"></a>2. Creación de certificados

Los clientes VPN tooauthenticate Azure usan certificados para Point-to-Site VPN. Cargar información de clave pública de Hola de tooAzure de certificado de raíz de Hola. clave pública de Hello, a continuación, se considera "confianza". Los certificados de cliente deben ser generados a partir de certificado de raíz de confianza de hello y, a continuación, se instala en cada equipo cliente en el almacén de certificados de usuario o Personal de certificados actual Hola. certificado de Hello es cliente de Hola de tooauthenticate usado cuando inicia una red virtual toohello de conexión. 

Si usa certificados autofirmados, se deben crear con parámetros específicos. Puede crear un certificado autofirmado mediante instrucciones de Hola para [PowerShell y Windows 10](vpn-gateway-certificates-point-to-site.md), o [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md). Es importante que siga los pasos de hello en estas instrucciones cuando se trabaja con los certificados raíz firmados y generar los certificados de cliente de Hola certificado raíz autofirmado. En caso contrario, los certificados de Hola que crea no serán compatibles con conexiones de P2S y recibirá un error de conexión.

### <a name="cer"></a>Parte 1: Obtener la clave pública de hello (.cer) para el certificado de raíz de Hola

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <a name="genclientcert"></a>Parte 2: Generación de un certificado de cliente

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="upload"></a>3. Cargar archivo de .cer del certificado de raíz de Hola

Una vez creada la puerta de enlace de hello, puede cargar Hola CER (que contiene información de clave pública de hello) para un tooAzure de certificado raíz de confianza. No cargar la clave privada de Hola Hola raíz certificado tooAzure. Una vez cargado el archivo a.cer, Azure puede usar a los clientes de tooauthenticate que han instalado un certificado de cliente generado a partir de certificado de raíz de confianza de Hola. Puede cargar los archivos de certificado raíz de confianza adicionales - tooa total de 20, más adelante, si es necesario.  

1. En hello **conexiones VPN** sección de página de hello para la red virtual, haga clic en hello **clientes** tooopen gráficos hello **Point-to-site VPN conexión** página.

  ![Clientes](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. En hello **conexiónPoint-to-site** página, haga clic en **administrar certificados** tooopen hello **certificados** página.<br>

  ![Página Certificados](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. En hello **certificados** página, haga clic en **cargar** tooopen hello **cargar certificado** página.<br>

    ![Página Cargar certificados](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/uploadcerts.png)<br>
4. Haga clic en el gráfico toobrowse de carpeta de hello para el archivo .cer de Hola. Seleccione el archivo hello, a continuación, haga clic en **Aceptar**. Actualización Hola página toosee Hola cargar certificado en hello **certificados** página.

  ![Carga del certificado](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/upload.png)<br>

## <a name="vpnclientconfig"></a>4. Configurar el cliente de Hola

tooconnect tooa red virtual con una VPN de sitio a punto, cada cliente debe instalar a un cliente de VPN de Windows nativo de paquete tooconfigure Hola. paquete de configuración de Hello configura el cliente de VPN de Windows nativo de hello con red virtual de hello configuración necesarios tooconnect toohello.

Puede usar Hola misma configuración de cliente VPN del paquete en cada equipo cliente, como versión de Hola coincida con la arquitectura de hello para el cliente de Hola. Para hello obtener lista de sistemas operativos cliente que son compatibles, vea hello [conexionesPoint-to-Site preguntas más frecuentes sobre](#faq) final Hola de este artículo.

### <a name="generateconfigpackage"></a>Parte 1: Generar e instalar el paquete de configuración de cliente VPN de Hola

1. En el portal de Azure, en Hola Hola **información general sobre** página para la red virtual, en **conexiones VPN**, haga clic en Hola Hola de gráficos tooopen cliente **Point-to-site VPN conexión** página.
2. En parte superior de Hola de hello **Point-to-site VPN conexión** página, haga clic en el paquete de descarga de hello correspondiente toohello sistema de operativo de cliente en el que se va a instalar:

  * Para los clientes de 64 bits, seleccione **Cliente de VPN (64 bits)**.
  * Para los clientes de 32 bits, seleccione **Cliente de VPN (32 bits)**.

  ![Descargar paquete de configuración de cliente de VPN](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/dlclient.png)<br>
3. Una vez que genera Hola empaquetado, descargue e instale en el equipo cliente. Si ve una ventana emergente de SmartScreen, haga clic en **Más información** y en **Ejecutar de todas formas**. También puede guardar Hola paquete tooinstall en otros equipos cliente.

### <a name="installclientcert"></a>Parte 2: Certificado de cliente de hello instalación

Si desea toocreate una P2S conexión desde un equipo cliente que no sea de Hola que utiliza certificados de cliente hello toogenerate, deberá tooinstall un certificado de cliente. Al instalar un certificado de cliente, necesita contraseña Hola que se creó cuando se exporta el certificado de cliente de Hola. Normalmente, esto es simplemente cuestión de doble clic en el certificado de hello e instalarla. Para más información, consulte [Instalación de un certificado de cliente exportado](vpn-gateway-certificates-point-to-site.md#install).

## <a name="connect"></a>5. Conectar tooAzure

### <a name="connect-tooyour-vnet"></a>Conectar tooyour red virtual

1. tooconnect tooyour de red virtual, en el equipo de cliente hello, navegar por las conexiones de tooVPN y encontrar la conexión de VPN de Hola que ha creado. Se denomina hello mismo nombre como la red virtual. Haga clic en **Conectar**. Puede aparecer un mensaje emergente que hace referencia el certificado de hello toousing. Si esto ocurre, haga clic en **continuar** toouse privilegios elevados.
2. En hello **conexión** página de estado, haga clic en **conectar** conexión de hello toostart. Si ve un **Seleccionar certificado** pantalla, compruebe que Hola cliente certificado que se muestra es Hola uno que desea toouse tooconnect. Si no es así, utilice certificado correcto de hello flecha de lista desplegable tooselect hello y, a continuación, haga clic en **Aceptar**.

  ![Conexión de cliente de VPN](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientconnect.png)
3. Se ha establecido la conexión.

  ![Conexión establecida](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>Solución de problemas de conexiones P2S

[!INCLUDE [verify-client-certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

### <a name="verifyvpnconnect"></a>Compruebe la conexión de VPN de Hola

1. tooverify que la conexión VPN esté activa, abra un símbolo del sistema con privilegios elevados y ejecute *ipconfig/all*.
2. Ver los resultados de Hola. Observe que la dirección IP de saludo recibida es una de las direcciones de hello dentro del intervalo de direcciones de conectividad de hello Point-to-Site que especificó cuando creó la red virtual. resultados de Hello deberían ser ejemplo toothis similar:

  ```
    PPP adapter VNet1:
        Connection-specific DNS Suffix .:
        Description.....................: VNet1
        Physical Address................:
        DHCP Enabled....................: No
        Autoconfiguration Enabled.......: Yes
        IPv4 Address....................: 192.168.130.2(Preferred)
        Subnet Mask.....................: 255.255.255.255
        Default Gateway.................:
        NetBIOS over Tcpip..............: Enabled
  ```

## <a name="connectVM"></a>Conectar máquina virtual de tooa

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-classic-include.md)]

## <a name="add"></a>Incorporación o eliminación de certificados raíz de confianza

Puede agregar y quitar certificados raíz de confianza de Azure. Cuando se quita un certificado raíz, los clientes que tienen un certificado generado a partir de esa raíz no será capaz de tooauthenticate y, por tanto, no será capaz de tooconnect. Si desea que un cliente tooauthenticate y conectarse, debe tooinstall genera un nuevo certificado de cliente de un certificado raíz de confianza tooAzure (cargado).

### <a name="addtrustedroot"></a>tooadd un certificado raíz de confianza

Puede sumar too20 confianza raíz certificado .cer archivos tooAzure. Para obtener instrucciones, consulte [sección 3 - archivo de .cer del certificado de raíz de carga hello](#upload).

### <a name="removetrustedroot"></a>tooremove un certificado raíz de confianza

1. En hello **conexiones VPN** sección de página de hello para la red virtual, haga clic en hello **clientes** tooopen gráficos hello **Point-to-site VPN conexión** página.

  ![Clientes](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. En hello **conexiónPoint-to-site** página, haga clic en **administrar certificados** tooopen hello **certificados** página.<br>

  ![Página Certificados](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. En hello **certificados** página, haga clic en hello puntos suspensivos siguiente toohello certificado que desee tooremove, a continuación, haga clic en **eliminar**.

  ![Eliminación de un certificado raíz](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deleteroot.png)<br>

## <a name="revokeclient"></a>Revocación de un certificado de cliente

Puede revocar certificados de cliente. podrá tooselectively lista de revocación de certificados de Hello denegar conectividad de punto a sitio basada en certificados de cliente individuales. Esto difiere de la forma en que se quita un certificado raíz de confianza. Si quita un .cer del certificado raíz de confianza de Azure, revoca el acceso de Hola para todos los certificados de cliente generado y firmado por certificado de raíz revocados Hola. Revocar un certificado de cliente, en lugar de certificado de raíz de hello, permite Hola otros certificados que se generaron desde el certificado de raíz de hello toocontinue toobe utilizado para la autenticación de conexión de hello Point-to-Site.

una práctica habitual Hello es toouse Hola certificado toomanage acceso a la raíz en los niveles de equipo u organización, durante el uso de certificados de cliente revocados para el control de acceso específica para los usuarios individuales.

### <a name="revokeclientcert"></a>toorevoke un certificado de cliente

Puede revocar un certificado de cliente mediante la adición de la lista de revocación de toohello Hola huella digital.

1. Recuperar la huella digital del certificado de cliente de Hola. Para obtener más información, consulte [Cómo: recuperar Hola huella digital de un certificado](https://msdn.microsoft.com/library/ms734695.aspx).
2. Copiar información hello tooa, editor de texto y quite todos los espacios para que sea una sola cadena continua.
3. Navegue toohello **'nombre de red virtual clásica' > conexión Point-to-site VPN > certificados** página y, a continuación, haga clic en **lista de revocación de** la página de lista de revocación de tooopen Hola. 
4. En hello **lista de revocación de** página, haga clic en **+ agregar certificado** tooopen hello **toorevocation lista de agregar certificado** página.
5. En hello **toorevocation lista de agregar certificado** , pegue la huella digital del certificado hello como una línea continua de texto, sin espacios en blanco. Haga clic en **Aceptar** final Hola de página Hola.
6. Una vez finalizada la actualización, certificado de hello ya no puede ser tooconnect usado. Los clientes que intentan tooconnect con este certificado, aparece un mensaje que indica que dicho certificado Hola ya no es válido.

## <a name="faq"></a>Preguntas más frecuentes sobre la conexión de punto a sitio

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Pasos siguientes
Una vez completada la conexión, puede agregar redes virtuales de máquinas virtuales tooyour. Consulte [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) para más información. toounderstand más información acerca de las redes y máquinas virtuales, consulte [información general de red de Azure y VM de Linux](../virtual-machines/linux/azure-vm-network-overview.md).
