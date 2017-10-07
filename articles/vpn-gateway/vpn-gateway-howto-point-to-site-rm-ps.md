---
title: "Conectar una red virtual de Azure con Point-to-Site tooan de equipo y la autenticación de certificados: PowerShell | Documentos de Microsoft"
description: "Conectarse de forma segura una red virtual de tooyour de equipo mediante la creación de una conexión de puerta de enlace de Point-to-Site VPN mediante la autenticación de certificado. En este artículo se aplica el modelo de implementación del Administrador de recursos de toohello y usa PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3eddadf6-2e96-48c4-87c6-52a146faeec6
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: b962e4b1946a4ae17d4eb2b920ed54437bc26b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-powershell"></a>Configurar una tooa de conexión de punto a sitio red virtual mediante la autenticación de certificado: PowerShell

Este artículo muestra cómo toocreate una red virtual con una conexión de punto a sitio en la implementación del Administrador de recursos de hello modelar con PowerShell. Esta configuración utiliza Hola de tooauthenticate certificados conecta el cliente. También puede crear esta configuración con una herramienta de implementación diferentes o un modelo de implementación seleccionando una opción diferente de hello lista siguiente:

> [!div class="op_single_selector"]
> * [Portal de Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Portal de Azure clásico](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

Una puerta de enlace VPN de punto a sitio (P2S) le permite crear una red virtual de tooyour de conexión segura desde un equipo cliente individual. Las conexiones de VPN de sitio a punto son útiles cuando se desea tooconnect tooyour red virtual desde una ubicación remota, como cuando trabajan a distancia desde casa o una conferencia. Una VPN P2S también es un toouse solución útil en lugar de una VPN de sitio a sitio cuando hay solo unos clientes que necesitan tooconnect tooa red virtual.

Usa P2S Hola Secure Socket de protocolo de túnel (SSTP), que es un protocolo VPN basada en SSL. Se establece una conexión VPN P2S, empiece por equipo de cliente de Hola.

![Conectar una red virtual de Azure - diagrama de sitio de punto de conexión de equipo tooan](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

Las conexiones de autenticación de certificado de punto a sitio requieren siguientes de hello:

* Una puerta de enlace de VPN RouteBased.
* Hola clave pública (archivo .cer) para un certificado raíz, que es cargado tooAzure. Una vez cargado el certificado de hello, se considera un certificado de confianza y se utiliza para la autenticación.
* Un certificado de cliente que se genera a partir de certificado de raíz de Hola e instalado en cada equipo cliente que se conectará toohello red virtual. Este certificado se usa para la autenticación de cliente.
* Un paquete de configuración de cliente de VPN. paquete de configuración de cliente VPN de Hello contiene información necesaria de Hola para hello cliente tooconnect toohello red virtual. paquete de Hello configura el cliente VPN existente hello es nativo toohello sistema operativo Windows. Cada cliente que se conecta debe configurarse mediante el paquete de configuración de Hola.

Las conexiones de punto a sitio no requieren un dispositivo VPN ni una dirección IP de acceso público local. Hola conexión VPN se crea a través de SSTP (Protocolo de túnel de sockets de seguros). En el lado del servidor hello, se admiten las versiones 1.0, 1.1 y 1.2 de SSTP. cliente de Hello decide qué toouse de versión. Para Windows 8.1 y versiones posteriores, SSTP usa 1.2 de forma predeterminada. 

Para obtener más información acerca de las conexiones punto a sitio, vea hello [Point-to-Site preguntas más frecuentes sobre](#faq) final Hola de este artículo.

## <a name="before-beginning"></a>Antes de comenzar

* Compruebe que tiene una suscripción a Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) o registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial).
* Instalar versión más reciente de Hola de hello cmdlets de PowerShell del Administrador de recursos de Azure. Para obtener más información acerca de cómo instalar los cmdlets de PowerShell, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

### <a name="example"></a>Valores del ejemplo

Puede usar toocreate de valores de ejemplo de Hola un entorno de prueba, o hacer referencia a valores de toothese toobetter comprender los ejemplos de hello en este artículo. Variables de Hola se establece en la sección [1](#declare) de artículo Hola. Puede utilizar pasos Hola como un ejemplo paso a paso y usar valores de hello sin modificarlas o cambiarlos tooreflect su entorno. 

* **Nombre: VNet1**
* **Espacio de direcciones: 192.168.0.0/16** y **10.254.0.0/16**<br>En este ejemplo, se usa más de un tooillustrate de espacio de dirección que esta configuración funciona con varios espacios de direcciones. Sin embargo, para esta configuración no se necesitan varios espacios de direcciones.
* **Nombre de subred: FrontEnd**
  * **Intervalo de direcciones de subred: 192.168.1.0/24**
* **Nombre de subred: BackEnd**
  * **Intervalo de direcciones de subred: 10.254.1.0/24**
* **Nombre de subred: GatewaySubnet**<br>nombre de la subred de Hello *GatewaySubnet* es obligatorio para toowork de puerta de enlace VPN de Hola.
  * **Intervalo de direcciones de GatewaySubnet: 192.168.200.0/24** 
* **Grupo de direcciones de clientes de VPN: 172.16.201.0/24**<br>Los clientes VPN que se conectan toohello red virtual con esta conexión de punto a sitio reciban una dirección IP de hello grupo de direcciones de cliente VPN.
* **Suscripción:** si tiene más de una suscripción, compruebe que está usando Hola correcto.
* **Grupo de recursos: TestRG**
* **Ubicación: este de EE. UU.**
* **Servidor DNS: Dirección IP** del servidor DNS de Hola que quiere toouse de resolución de nombres.
* **Nombre de puerta de enlace: Vnet1GW**
* **Nombre IP pública: VNet1GWPIP**
* **VPNType: RouteBased** 

## <a name="declare"></a>1. Inicio de sesión y establecimiento de variables

En esta sección, inicie sesión y declarar los valores de hello utilizados para esta configuración. Hola declara valores se utilizan en las secuencias de comandos de ejemplo de Hola. Cambiar tooreflect de valores de hello en su propio entorno. O bien, puede usar hello declarado valores y seguir los pasos de Hola como un ejercicio.

1. Abra la consola de PowerShell con privilegios elevados e inicie sesión tooyour cuenta de Azure. Este cmdlet le pide las credenciales de inicio de sesión de Hola. Después de iniciar sesión, descarga la configuración de la cuenta para que estén disponible tooAzure PowerShell.

  ```powershell
  Login-AzureRmAccount
  ```
2. Obtenga una lista de las suscripciones de Azure.

  ```powershell
  Get-AzureRmSubscription
  ```
3. Especifique que desea toouse de suscripción de Hola.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. Declare las variables de Hola que desea toouse. Usar hello según muestra, sustituyendo los valores de hello para su propio cuando sea necesario.

  ```powershell
  $VNetName  = "VNet1"
  $FESubName = "FrontEnd"
  $BESubName = "Backend"
  $GWSubName = "GatewaySubnet"
  $VNetPrefix1 = "192.168.0.0/16"
  $VNetPrefix2 = "10.254.0.0/16"
  $FESubPrefix = "192.168.1.0/24"
  $BESubPrefix = "10.254.1.0/24"
  $GWSubPrefix = "192.168.200.0/26"
  $VPNClientAddressPool = "172.16.201.0/24"
  $RG = "TestRG"
  $Location = "East US"
  $DNS = "10.1.1.3"
  $GWName = "VNet1GW"
  $GWIPName = "VNet1GWPIP"
  $GWIPconfName = "gwipconf"
  ```

## <a name="ConfigureVNet"></a>2. Configuración de una red virtual

1. Cree un grupo de recursos.

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. Crear configuraciones de subred para la red virtual de hello, asignarles de hello *front-end*, *back-end*, y *GatewaySubnet*. Estos prefijos deben formar parte del programa Hola espacio de direcciones de red virtual que declara.

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. Crear red virtual de Hola.

  En este ejemplo, el servidor DNS de hello es opcional. La especificación de un valor no crea un servidor DNS nuevo. Hello dirección IP del servidor DNS que especifique debe ser un servidor DNS que pueda resolver nombres de Hola para los recursos de saludo a que se está conectando. En este ejemplo, se usa una dirección IP privada, pero es probable que esto no es Hola dirección IP del servidor DNS. Ser seguro toouse sus propios valores.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. Especificar las variables de hello para la red virtual de Hola que creó.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. Una puerta de enlace VPN debe tener una dirección IP pública. Solicitar el recurso de dirección IP hello y, a continuación, hacer referencia tooit al crear la puerta de enlace de red virtual. dirección IP de Hola se asigna dinámicamente toohello recursos cuando se crea la puerta de enlace VPN de Hola. Actualmente, VPN Gateway solo admite la asignación de direcciones IP públicas *dinámicas*. No se puede solicitar una asignación de direcciones IP públicas estáticas. Sin embargo, no significa que se cambia la dirección IP de hello después de que se le ha asignado tooyour puerta de enlace VPN. cambios en la dirección IP pública hello cuando se Hola puerta de enlace de única vez de Hola se elimina y vuelve a crear. No cambia cuando se cambia el tamaño, se restablece o se realizan actualizaciones u otras operaciones de mantenimiento interno de una puerta de enlace VPN.

  Solicite una dirección IP pública asignada de forma dinámica.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <a name="creategateway"></a>3. Crear puerta de enlace VPN de Hola

Configurar y crear la puerta de enlace de red virtual de hello para la red virtual.

* Hola *- el GatewayType* debe ser **Vpn** hello y *- VpnType* debe ser **RouteBased**.
* Una puerta de enlace VPN puede tardar hasta too45 toocomplete de minutos, dependiendo de hello [sku de puerta de enlace](vpn-gateway-about-vpn-gateway-settings.md) seleccione.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <a name="addresspool"></a>4. Agregar grupo de direcciones de cliente VPN de Hola

Una vez finaliza la creación de puerta de enlace VPN de hello, puede agregar grupo de direcciones de cliente VPN de Hola. Hola grupo de direcciones de cliente VPN es intervalo Hola desde el cual los clientes VPN de Hola reciban una dirección IP al conectarse. Usar un intervalo de direcciones IP privadas que no se superponen con ubicación local de Hola que se conectan desde, o con hello red virtual que desea tooconnect a. En este ejemplo, hello grupo de direcciones de cliente VPN se declara como un [variable](#declare) en el paso 1.

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <a name="Certificates"></a>5. Generación de certificados

Los clientes VPN tooauthenticate Azure usan certificados para Point-to-Site VPN. Cargar información de clave pública de Hola de tooAzure de certificado de raíz de Hola. clave pública de Hello, a continuación, se considera "confianza". Los certificados de cliente deben ser generados a partir de certificado de raíz de confianza de hello y, a continuación, se instala en cada equipo cliente en el almacén de certificados de usuario o Personal de certificados actual Hola. certificado de Hello es cliente de Hola de tooauthenticate usado cuando inicia una red virtual toohello de conexión. 

Si usa certificados autofirmados, se deben crear con parámetros específicos. Puede crear un certificado autofirmado mediante instrucciones de Hola para [PowerShell y Windows 10](vpn-gateway-certificates-point-to-site.md), o bien, si no tiene Windows 10, puede usar [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md). Es importante que siga los pasos de hello en instrucciones de hello al generar certificados raíz autofirmados y certificados de cliente. En caso contrario, no serán compatibles con conexiones de P2S certificados Hola que generar y recibirá un error de conexión.

### <a name="cer"></a>1. Obtener el archivo .cer de hello para el certificado de raíz de Hola

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <a name="generate"></a>2. Generación de un certificado de cliente

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="upload"></a>6. Cargar información de clave pública de hello raíz certificado

Compruebe que ha terminado de crear la puerta de enlace VPN. Una vez que se ha completado, puede cargar Hola CER (que contiene información de clave pública de hello) para un tooAzure de certificado raíz de confianza. Una vez cargado el archivo a.cer, Azure puede usar a los clientes de tooauthenticate que han instalado un certificado de cliente generado a partir de certificado de raíz de confianza de Hola. Puede cargar los archivos de certificado raíz de confianza adicionales - tooa total de 20, más adelante, si es necesario.

1. Declarar la variable de hello para el nombre del certificado, reemplazando el valor de Hola por los suyos propios.

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. Reemplace la ruta de acceso de archivo de hello con sus propios y, a continuación, ejecutar los cmdlets de Hola.

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. Cargar hello tooAzure de información de clave pública. Una vez que se carga la información del certificado hello, Azure tiene en cuenta este toobe un certificado raíz de confianza.

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <a name="clientconfig"></a>7. Descargar paquete de configuración de cliente VPN de Hola

tooconnect tooa red virtual con una VPN de sitio a punto, cada cliente debe instalar un paquete de configuración de cliente que se configura el cliente VPN nativo que Hola con los valores de hello y archivos de red virtual de toohello tooconnect necesarios. paquete de configuración de cliente VPN de Hello configura el cliente de VPN de Windows nativo hello, pero no instala un cliente VPN de nuevo o diferente. 

Puede usar Hola misma configuración de cliente VPN del paquete en cada equipo cliente, como versión de Hola coincida con la arquitectura de hello para el cliente de Hola. Para hello obtener lista de sistemas operativos cliente que son compatibles, vea hello [conexionesPoint-to-Site preguntas más frecuentes sobre](#faq) final Hola de este artículo.

1. Una vez creada la puerta de enlace de hello, puede generar y descargar el paquete de configuración de cliente de Hola. En este ejemplo, se descarga el paquete de Hola para los clientes de 64 bits. Si desea que el cliente de 32 bits de hello toodownload, reemplace 'Amd64' con 'x86'. También puede descargar el cliente VPN de hello mediante el uso de hello portal de Azure.

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. Copie y pegue el vínculo de Hola que se devuelve tooa explorador toodownload Hola paquete web, teniendo cuidado de las comillas de hello tooremove que rodea el vínculo de Hola. 
3. Descargue e instale el paquete de hello en el equipo cliente de Hola. Si ve una ventana emergente de SmartScreen, haga clic en **Más información** y en **Ejecutar de todas formas**. También puede guardar Hola paquete tooinstall en otros equipos cliente.
4. En el equipo de cliente hello, vaya demasiado**configuración de red** y haga clic en **VPN**. Hola conexión VPN muestra nombre Hola de red virtual de Hola que se conecta a.

## <a name="clientcertificate"></a>8. Instalación de un certificado de cliente exportado

Si desea toocreate una P2S conexión desde un equipo cliente que no sea de Hola que utiliza certificados de cliente hello toogenerate, deberá tooinstall un certificado de cliente. Al instalar un certificado de cliente, necesita contraseña Hola que se creó cuando se exporta el certificado de cliente de Hola. Normalmente, es simplemente cuestión de doble clic en el certificado de hello e instalarla.

Asegúrese de que se exportó el certificado de cliente de Hola como un .pfx junto con la cadena de certificados completa de hello (que es el valor predeterminado de hello). En caso contrario, no está presente en el equipo de cliente hello información del certificado de raíz de Hola y cliente hello no será capaz de tooauthenticate correctamente. Para más información, consulte [Instalación de un certificado de cliente exportado](vpn-gateway-certificates-point-to-site.md#install). 

## <a name="connect"></a>9. Conectar tooAzure

1. tooconnect tooyour de red virtual, en el equipo de cliente hello, navegar por las conexiones de tooVPN y encontrar la conexión de VPN de Hola que ha creado. Se denomina hello mismo nombre como la red virtual. Haga clic en **Conectar**. Puede aparecer un mensaje emergente que hace referencia el certificado de hello toousing. Haga clic en **continuar** toouse privilegios elevados. 
2. En hello **conexión** página de estado, haga clic en **conectar** conexión de hello toostart. Si ve un **Seleccionar certificado** pantalla, compruebe que Hola cliente certificado que se muestra es Hola uno que desea toouse tooconnect. Si no es así, utilice certificado correcto de hello flecha de lista desplegable tooselect hello y, a continuación, haga clic en **Aceptar**.

  ![TooAzure conecta el cliente VPN](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. Se ha establecido la conexión.

  ![Conexión establecida](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>Solución de problemas de conexiones P2S

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <a name="verify"></a>10. Comprobación de la conexión

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

## <a name="addremovecert"></a>Adición o eliminación de un certificado raíz

Puede agregar y quitar certificados raíz de confianza de Azure. Cuando se quita un certificado raíz, los clientes que tienen un certificado generado a partir de certificado de raíz de hello no se pueden autenticar y no será capaz de tooconnect. Si desea que un cliente tooauthenticate y conectarse, debe tooinstall genera un nuevo certificado de cliente de un certificado raíz de confianza tooAzure (cargado).

### <a name="addtrustedroot"></a>tooadd un certificado raíz de confianza

Puede sumar too20 raíz certificado .cer archivos tooAzure. Hola siguientes pasos le indican ayudan a agregar un certificado raíz:

#### <a name="certmethod1"></a>Método 1

Se trata de tooupload de método más eficaz de hello un certificado raíz.

1. Preparar tooupload de archivo .cer hello:

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. Cargar archivo hello. Solo puede cargar un archivo a la vez.

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. tooverify que Hola cargado el archivo de certificado:

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <a name="certmethod2"></a>Método 2

Este método es tiene pasos más que el método 1, pero tiene Hola el mismo resultado. Se incluye por si tuviera datos del certificado tooview Hola.

1. Crear y preparar Hola nueva raíz certificado tooadd tooAzure. Exportar la clave pública de hello como Base64 codificado X.509 (. (CER) y ábralo con un editor de texto. Copiar valores de hello, como se muestra en el siguiente ejemplo de Hola:

  ![certificado](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > Cuando se copian datos de certificado de hello, asegúrese de que copia texto hello como una línea continua sin retornos de carro o avances de línea. Deberá toomodify la vista mediante too'Show de editor de texto hello símbolos/mostrar toosee Hola de carro todos los caracteres devuelve y saltos de línea.
  >
  >

2. Especificar el nombre del certificado de Hola y la información clave como una variable. Reemplace Hola información con su cuenta, como se muestra en hello ejemplo siguiente:

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. Agregar nuevo certificado de raíz Hola. Solo puede agregar un certificado raíz a la vez.

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. Puede comprobar el que certificado nuevo Hola se agregó correctamente utilizando el siguiente ejemplo de Hola:

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <a name="removerootcert"></a>tooremove un certificado raíz

1. Declare las variables de Hola.

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. Quitar certificado de Hola.

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. Hola de uso después de tooverify de ejemplo que Hola certificado se eliminó correctamente.

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <a name="revoke"></a>Revocación de un certificado de cliente

Puede revocar certificados de cliente. podrá tooselectively lista de revocación de certificados de Hello denegar conectividad de punto a sitio basada en certificados de cliente individuales. Esto difiere de la forma en que se quita un certificado raíz de confianza. Si quita un .cer del certificado raíz de confianza de Azure, revoca el acceso de Hola para todos los certificados de cliente generado y firmado por certificado de raíz revocados Hola. Revocar un certificado de cliente, en lugar de certificado de raíz de hello, permite Hola otros certificados que se generaron desde el certificado de raíz de hello toocontinue toobe utilizado para la autenticación.

una práctica habitual Hello es toouse Hola certificado toomanage acceso a la raíz en los niveles de equipo u organización, durante el uso de certificados de cliente revocados para el control de acceso específica para los usuarios individuales.

### <a name="revokeclientcert"></a>toorevoke un certificado de cliente

1. Recuperar la huella digital del certificado de cliente de Hola. Para obtener más información, consulte [cómo tooretrieve Hola huella digital de un certificado](https://msdn.microsoft.com/library/ms734695.aspx).
2. Copiar información hello tooa, editor de texto y quite todos los espacios para que sea una sola cadena continua. Esta cadena se declara como una variable en el paso siguiente de saludo.
3. Declare las variables de Hola. Asegúrese de que ha recuperado la huella digital Hola de toodeclare seguro en el paso anterior de Hola.

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. Agregue Hola huella digital toohello lista de certificados revocados. Vea "Correcto" cuando se ha agregado la huella digital de Hola.

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. Comprobar que huella digital Hola se agregó toohello lista de revocación de certificados.

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. Una vez agregada la huella digital de hello, certificado de hello ya no puede ser tooconnect usado. Los clientes que intentan tooconnect con este certificado, aparece un mensaje que indica que dicho certificado Hola ya no es válido.

### <a name="reinstateclientcert"></a>tooreinstate un certificado de cliente

Puede volver a aplicar un certificado de cliente mediante la eliminación de huella digital de hello en lista de Hola de certificados de cliente revocados.

1. Declare las variables de Hola. Asegúrese de que se declare Hola correcto la huella digital de certificado de Hola que quiere que tooreinstate.

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. Quitar huella digital del certificado Hola de lista de revocación de certificados de Hola.

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. Compruebe si la huella digital de Hola se quita de hello revocado lista.

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <a name="faq"></a>Preguntas más frecuentes sobre la conexión de punto a sitio

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Pasos siguientes
Una vez completada la conexión, puede agregar redes virtuales de máquinas virtuales tooyour. Consulte [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) para más información. toounderstand más información acerca de las redes y máquinas virtuales, consulte [información general de red de Azure y VM de Linux](../virtual-machines/linux/azure-vm-network-overview.md).
