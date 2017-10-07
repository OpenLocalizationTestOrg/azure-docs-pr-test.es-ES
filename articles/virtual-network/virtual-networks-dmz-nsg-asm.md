---
title: 'aaaAzure DMZ ejemplo: crear una red Perimetral Simple con NSG | Documentos de Microsoft'
description: "Creación de una red perimetral con grupos de seguridad de red"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: f8622b1d-c07d-4ea6-b41c-4ae98d998fff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 32a40a8dc7539c4c7293988e6c36e5e32ef11045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a>Ejemplo 1: crear una red perimetral simple mediante grupos de seguridad de red con PowerShell clásico
[Devolver toohello página de prácticas recomendadas de seguridad límite][HOME]

> [!div class="op_single_selector"]
> * [Plantilla de Resource Manager](virtual-networks-dmz-nsg.md)
> * [Clásico: PowerShell](virtual-networks-dmz-nsg-asm.md)
> 
>

En este ejemplo se crea una red perimetral primitiva con cuatro servidores Windows y grupos de seguridad de red. Este ejemplo describe cada uno de los tooprovide de comandos de PowerShell relevante de hello una comprensión más profunda de cada paso. También hay un escenario de tráfico sección tooprovide una detallada paso a paso cómo tráfico pasa a través de las capas de defensa en Hola Hola red Perimetral. Por último, en la sección de referencias de hello es código completo de Hola e instrucción toobuild este entorno tootest y experimentar con diferentes escenarios. 

![Red perimetral de entrada con grupo de seguridad de red][1]

## <a name="environment-description"></a>Descripción del entorno
En este ejemplo, una suscripción contiene Hola recursos siguientes:

* Dos servicios en la nube: "FrontEnd001" y "BackEnd001"
* Una red virtual, “CorpNetwork”, con dos subredes, “FrontEnd” y “BackEnd”
* Un grupo de seguridad de red que está aplicada tooboth subredes
* Un servidor Windows que representa un servidor de aplicaciones web ("IIS01")
* Dos servidores Windows que representan servidores back-end de aplicaciones ("AppVM01", "AppVM02")
* Un servidor Windows que representa un servidor DNS ("DNS01")

En la sección de referencias de hello, hay una secuencia de comandos de PowerShell que se basa la mayor parte del entorno de hello descrita en este ejemplo. Hola de crear las máquinas virtuales y redes virtuales, aunque se realizan mediante el script de ejemplo de Hola, no se describen en detalle en este documento. 

entorno de hello toobuild;

1. Guardar archivo de xml de configuración Hola red incluido en la sección de referencias de hello (actualizada con nombres, la ubicación y el escenario de hello dada de toomatch de direcciones IP)
2. Variables de usuario de actualización hello en hello toomatch Hola entorno Hola de script es toobe ejecutarán (suscripciones, los nombres de servicio, etcetera.)
3. Ejecutar script de Hola en PowerShell

>[!Note]
>región Hola indicado en el script de PowerShell de Hola debe coincidir con la región Hola indicado en el archivo de xml de configuración de red de Hola.
>
>

Una vez que se ejecuta correctamente adicional el script de Hola pasos opcionales pueden tener, en la sección de referencias de hello son dos de las secuencias de comandos tooset seguridad hello web y servidor de aplicaciones con una tooallow de aplicación web simple pruebas con esta configuración de red Perimetral.

Hello secciones siguientes proporcionan una descripción detallada de los grupos de seguridad de red y cómo funcionan en este ejemplo recorriendo líneas de clave de secuencia de comandos de PowerShell de Hola.

## <a name="network-security-groups-nsg"></a>Grupos de seguridad de red (NSG)
En este ejemplo, se crea un grupo de seguridad de red y se cargan después seis reglas. 

> [!TIP]
> Por lo general, debe crear primero las reglas específicas de "Permitir" y, a continuación, Hola reglas más genéricas de "Denegar" última. Hola tenga asignada la prioridad determina qué reglas se evalúan primero. Una vez que el tráfico se encuentra la regla específica de tooapply tooa, no se evalúa ninguna otra regla. Se pueden aplicar reglas NSG en la vista en hello dirección entrante o saliente (desde la perspectiva de Hola de subred de hello).
> 
> 

Mediante declaración, se regeneran Hola siguiendo las reglas para el tráfico entrante:

1. Se permite el tráfico DNS interno (puerto 53)
2. Se permite el tráfico RDP (puerto 3389) de hello Internet tooany VM
3. Se permite el tráfico HTTP (puerto 80) del servidor de hello Internet tooweb (IIS01)
4. Se permite cualquier tráfico (todos los puertos) del IIS01 tooAppVM1
5. Todo (todos los puertos) el tráfico de hello Internet toohello se deniega todo red virtual (tanto en las subredes)
6. Se deniega todo (todos los puertos) el tráfico de subred de back-end de hello front-end subred toohello

Con estas subredes de enlazado tooeach reglas, si una solicitud HTTP es entrante desde el servidor web de hello Internet toohello, ambas reglas 3 (permitir) y 5 (denegar) aplicaría, pero dado que la regla 3 tiene mayor prioridad solo aplicaría y regla 5 podría no entran en juego. Por lo tanto solicitud HTTP de hello podría permitirse a toohello servidor de web. Si ese mismo tráfico estaba intentando server DNS01 de tooreach hello, regla 5 (Deny) sería Hola primera hello y tooapply el tráfico no estarían permitido a toopass toohello server. Regla 6 (Deny) bloques de subred de front-end de Hola de hablar de subred de back-end de toohello (excepto el tráfico permitido en las reglas 1 y 4), este conjunto de reglas protege la red de back-end de hello en caso de que una aplicación atacante pone en peligro hello web en hello front-end, el atacante de hello sería ha limitado toohello acceso back-end "protegido" red (solo tooresources expuesta en el servidor de hello AppVM01).

Hay una regla de salida predeterminada que permite el tráfico de salida toohello internet. En este ejemplo, permitimos el tráfico saliente y no modificamos las reglas de salida. toolock hacia abajo el tráfico en ambas direcciones, enrutamiento de definido por usuario es obligatorio y se explora en "Ejemplo 3" en hello [página de prácticas recomendadas de seguridad límite][HOME].

Cada regla se explica con más detalle como sigue (**Nota**: cualquier elemento de hello sigue el principio de la lista con un signo de dólar (por ejemplo: $NSGName) es una variable definida por el usuario desde un script de Hola en la sección de referencia de Hola de este documento):

1. En primer lugar un grupo de seguridad de red debe compilarse reglas de Hola toohold:

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. la primera regla en este ejemplo de Hola permite el tráfico DNS entre todos los servidores DNS de toohello redes internas de subred de back-end de Hola. regla de Hello tiene algunos parámetros importantes:
   
   * "Type" indica en qué dirección del flujo de tráfico esta entrada surte efecto. dirección de Hello es desde la perspectiva de Hola de subred de Hola o una máquina Virtual (en función de donde está enlazado este GSN). Por lo tanto si tipo es "Inbound" y está accediendo al tráfico de subred de Hola, Hola regla se aplicará y tráfico que sale de la subred de hello no se verían afectado por esta regla.
   * "Priority" establece el orden de hello en el que se evalúa un flujo de tráfico. Hola inferior Hola número Hola Hola prioridad. Cuando una regla aplica tooa flujo de tráfico específico, no se procesa ninguna otra regla. Por tanto, si una regla con prioridad 1 permite el tráfico y una regla con prioridad 2 deniega el tráfico y ambas reglas aplican tootraffic, ¿se permite el tráfico de hello tooflow (puesto regla 1 no tenía una prioridad más alta entra en vigor y no se aplica ninguna otra regla).
   * "Action" indica si se bloquea o se permite el tráfico al que afecta esta regla.

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. Esta regla permite tooflow de tráfico RDP de hello internet toohello el puerto RDP en cualquier servidor de hello enlazado subred. Esta regla usa dos tipos especiales de prefijos de dirección: "VIRTUAL_NETWORK" e "INTERNET". Estas etiquetas son un tooaddress fácilmente una categoría mayor de prefijos de dirección.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. Esta regla permite que servidor de web de hello toohit de tráfico de internet entrante. Esta regla no cambia el comportamiento de enrutamiento Hola. regla de Hello solo permite el tráfico destinado a IIS01 toopass. Por lo tanto si el tráfico de Internet Hola tenía el servidor de web de hello como su destino de esta regla se permitirlo y detener el procesamiento de más reglas. (En la regla de hello con prioridad 140 todos los demás tráfico entrante de internet se bloquea). Si sólo está procesando el tráfico HTTP, esta regla podría ser más restringido tooonly Permitir destino puerto 80.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet too$VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. Esta regla permite toopass de tráfico desde el servidor de hello IIS01 toohello AppVM01 server, una regla posterior bloquea todo el tráfico de otros tooBackend front-end. tooimprove esta regla, si se conoce el puerto de Hola que debe agregarse. Por ejemplo, si el servidor IIS de hello está alcanzando solo SQL Server en AppVM01, intervalo de puertos de destino de hello debe cambiarse de "*" (Any) too1433 (Hola puerto de SQL) lo que permite una menor superficie expuesta a ataques entrantes en AppVM01 debe alguna vez verse comprometida la aplicación web de Hola.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] too$VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. Esta regla deniega el tráfico de los servidores de tooany de internet de hello en red Hola. Con las reglas de hello en prioridad 110 y 120, el efecto de hello es tooallow solo internet tráfico toohello firewall de entrada y puertos RDP en servidores y todo lo demás bloquea. Esta regla es la regla de notificaciones de "error" tooblock todos los flujos inesperados.
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $VNetName VNet from hello Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. regla de final de Hello deniega el tráfico de subred de back-end de hello front-end subred toohello. Puesto que esta regla es una regla de sola entrada, se permite el tráfico inverso (de hello back-end toohello front-end).

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a>Escenarios de tráfico
#### <a name="allowed-internet-tooweb-server"></a>(*Permitido*) servidor de Internet tooweb
1. Un usuario de Internet solicita una página HTTP desde FrontEnd001.CloudApp.Net (servicio en la nube accesible desde Internet).
2. En la nube tráfico del servicio pasa a través de un extremo abierto en el puerto 80 hacia IIS01 (servidor web de hello)
3. La subred front-end comienza el procesamiento de las reglas de entrada:
   1. 1 de la regla de NSG (DNS) no se aplica, mover toonext regla
   2. 2 de la regla de NSG (RDP) no se aplica, mover toonext regla
   3. Aplicar NSG regla 3 (tooIIS01 Internet), el tráfico es el procesamiento de reglas permitidas, detenga
4. Tráfico alcanza el dirección IP interna del servidor web de hello IIS01 (10.0.1.5)
5. Iis01 escucha el tráfico de web, recibe esta solicitud y comienza a procesar la solicitud de Hola
6. Iis01 pide Hola SQL Server en AppVM01 información
7. Puesto que no hay reglas de salida en la subred front-end, se permite el tráfico.
8. subred de back-end de Hello comienza el procesamiento de la regla de entrada:
   1. 1 de la regla de NSG (DNS) no se aplica, mover toonext regla
   2. 2 de la regla de NSG (RDP) no se aplica, mover toonext regla
   3. Regla de NSG 3 (tooFirewall Internet) no se aplica, mover toonext regla
   4. Aplicar NSG regla 4 (IIS01 tooAppVM01), el tráfico es el procesamiento de reglas permitidas, detenga
9. AppVM01 recibe Hola consulta SQL y responde
10. Dado que no hay ninguna regla de salida en la subred de back-end de hello, se permite la respuesta de Hola
11. La subred front-end comienza el procesamiento de las reglas de entrada:
    1. No hay ninguna regla NSG que se aplica tooInbound tráfico de subred de front-end del toohello Hola de subred de back-end, por lo que no se aplica ninguno de reglas NSG Hola
    2. Hola regla predeterminada del sistema permitiendo el tráfico entre subredes permitiría este tráfico, por lo que se permite el tráfico de Hola.
12. servidor IIS de Hello recibe la respuesta SQL de Hola y completa respuesta HTTP de Hola y envía toohello solicitante
13. Dado que no hay ninguna regla de salida en la subred de front-end de Hola Hola se permita respuesta y hello internet usuario recibe hello web página solicitada.

#### <a name="allowed-rdp-toobackend"></a>(*Permitido*) toobackend RDP
1. Administrador del servidor en internet solicita tooAppVM01 de sesión RDP en BackEnd001.CloudApp.Net:xxxxx donde xxxxx es el número de puerto de hello asignada aleatoriamente para tooAppVM01 RDP (puerto Hola asignado se puede encontrar en el portal de Azure de Hola o a través de PowerShell)
2. La subred back-end comienza el procesamiento de las reglas de entrada:
   1. 1 de la regla de NSG (DNS) no se aplica, mover toonext regla
   2. Se aplica la regla 2 (RDP) de grupo de seguridad de red, se permite el tráfico, detener el procesamiento de las reglas.
3. No hay reglas de salida, se aplican las reglas predeterminadas y se permite el tráfico de retorno.
4. La sesión RDP está habilitada.
5. Mensajes de AppVM01 Hola nombre de usuario y contraseña

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a>(*Permitido*) Búsqueda de DNS del servidor web en el servidor DNS
1. Web necesidades de servidor, IIS01, fuente de distribución de datos en www.data.gov, pero necesita tooresolve Hola dirección.
2. Hola configuración de red para las listas de red virtual de hello DNS01 (10.0.2.4 de subred de back-end de hello) como servidor DNS principal de hello, IIS01 envía Hola DNS solicitud tooDNS01
3. No hay reglas de salida en la subred front-end, se permite el tráfico.
4. La subred back-end comienza el procesamiento de las reglas de entrada:
   * Se aplica la regla 1 (DNS) de grupo de seguridad de red, se permite el tráfico, detener el procesamiento de las reglas.
5. Servidor DNS recibe la solicitud de Hola
6. Servidor DNS no tiene dirección de hello en caché y pide un servidor DNS raíz en hello internet
7. No hay reglas de salida en la subred back-end, se permite el tráfico.
8. Se responde el servidor DNS de Internet, ya que esta sesión se ha iniciado internamente, se permite la respuesta de Hola
9. Servidor DNS almacena en caché la respuesta de Hola y responde tooIIS01 de espera de solicitud inicial toohello
10. No hay reglas de salida en la subred back-end, se permite el tráfico.
11. La subred front-end comienza el procesamiento de las reglas de entrada:
    1. No hay ninguna regla NSG que se aplica tooInbound tráfico de subred de front-end del toohello Hola de subred de back-end, por lo que no se aplica ninguno de reglas NSG Hola
    2. Hola regla predeterminada del sistema permitiendo el tráfico entre subredes permitiría este tráfico por lo que se permite el tráfico de Hola
12. Iis01 recibe respuesta hello DNS01

#### <a name="allowed-web-server-access-file-on-appvm01"></a>(*Permitido*) Archivo de acceso del servidor web en AppVM01
1. IIS01 solicita un archivo en AppVM01
2. No hay reglas de salida en la subred front-end, se permite el tráfico.
3. subred de back-end de Hello comienza el procesamiento de la regla de entrada:
   1. 1 de la regla de NSG (DNS) no se aplica, mover toonext regla
   2. 2 de la regla de NSG (RDP) no se aplica, mover toonext regla
   3. Regla de NSG 3 (tooIIS01 Internet) no se aplica, mover toonext regla
   4. Aplicar NSG regla 4 (IIS01 tooAppVM01), el tráfico es el procesamiento de reglas permitidas, detenga
4. AppVM01 recibe la solicitud de Hola y responde con el archivo (suponiendo que se autoriza el acceso)
5. Dado que no hay ninguna regla de salida en la subred de back-end de hello, se permite la respuesta de Hola
6. La subred front-end comienza el procesamiento de las reglas de entrada:
   1. No hay ninguna regla NSG que se aplica tooInbound tráfico de subred de front-end del toohello Hola de subred de back-end, por lo que no se aplica ninguno de reglas NSG Hola
   2. Hola regla predeterminada del sistema permitiendo el tráfico entre subredes permitiría este tráfico, por lo que se permite el tráfico de Hola.
7. servidor IIS de Hello recibe el archivo hello

#### <a name="denied-web-toobackend-server"></a>(*Denegado*) servidor de Web toobackend
1. Tooaccess un archivo en AppVM01 a través de hello BackEnd001.CloudApp.Net servicio trata de un usuario de internet
2. Dado que no hay ningún extremo abierto para el recurso compartido de archivos, este tráfico no pasaría Hola servicio en la nube y no llegar a servidor hello
3. Si los puntos de conexión de hello estaban abiertos por algún motivo, la regla de NSG 5 (Internet tooVNet) bloquearían este tráfico

#### <a name="denied-web-dns-look-up-on-dns-server"></a>(*Denegado*) Búsqueda de DNS web en el servidor DNS
1. Un usuario de internet intenta toolook un registro de DNS interna en DNS01 a través de hello BackEnd001.CloudApp.Net servicio
2. Dado que no hay ningún extremo abierto para DNS, este tráfico no pasaría Hola servicio en la nube y no llegar a servidor hello
3. Si los puntos de conexión de hello estaban abiertos por algún motivo, la regla de NSG 5 (Internet tooVNet) bloquearían este tráfico (Nota: esa regla 1 (DNS) no se aplicarían por dos motivos, primera dirección de origen de hello es Hola internet, esta regla solo aplica toohello red virtual local como Hola de origen, también Esta regla es una regla de permiso, por lo que nunca podría denegar el tráfico)

#### <a name="denied-web-toosql-access-through-firewall"></a>(*Denegado*) Web tooSQL acceso a través del firewall
1. Un usuario de Internet solicita los datos SQL desde FrontEnd001.CloudApp.Net (servicio en la nube accesible desde Internet).
2. Dado que no hay ningún extremo abierto para SQL, este tráfico no pasaría Hola servicio en la nube y no llegar a firewall de Hola
3. Si los puntos de conexión estaban abiertos por algún motivo, subred de front-end de hello comienza el procesamiento de la regla de entrada:
   1. 1 de la regla de NSG (DNS) no se aplica, mover toonext regla
   2. 2 de la regla de NSG (RDP) no se aplica, mover toonext regla
   3. Aplicar NSG regla 3 (tooIIS01 Internet), el tráfico es el procesamiento de reglas permitidas, detenga
4. Tráfico alcanza el dirección IP interna de hello IIS01 (10.0.1.5)
5. Iis01 no está escuchando en el puerto 1433, por lo que no hay ninguna solicitud de toohello de respuesta

## <a name="conclusion"></a>Conclusión
En este ejemplo es una forma relativamente simple y sencillo de aislar la subred de back-end de Hola de tráfico entrante.

Puede encontrar más ejemplos y una descripción general de los límites de seguridad de red [aquí][HOME].

## <a name="references"></a>Referencias
### <a name="main-script-and-network-config"></a>Script principal y configuración de red
Guardar Hola Script completo en un archivo de script de PowerShell. Guardar Hola configuración de red en un archivo denominado "NetworkConf1.xml."
Modificar variables definidas por el usuario de hello como script de Hola necesarios y que se ejecutan.

#### <a name="full-script"></a>Script completo
Esta secuencia de comandos mostrarán, en función de variables definidas por el usuario de hello;

1. Conectar tooan suscripción de Azure
2. Crear una cuenta de almacenamiento
3. Crear una red virtual y dos subredes tal como se define en el archivo de configuración de red de Hola
4. Creación de cuatro máquinas virtuales de Windows Server
5. Configuración del grupo de seguridad de red, incluido lo siguiente:
   * Creación de un grupo de seguridad de red
   * Rellenado con reglas
   * Enlace hello NSG toohello las subredes correspondientes

Este script de PowerShell debe ejecutarse localmente en un equipo o servidor conectado a Internet.

> [!IMPORTANT]
> Cuando se ejecuta este script, puede haber advertencias u otros mensajes informativos que se muestran en PowerShell. Solo los mensajes de error indicados en rojo son motivo de preocupación.
> 
>

```PowerShell
<# 
 .SYNOPSIS
  Example of Network Security Groups in an isolated network (Azure only, no hybrid connections)

 .DESCRIPTION
  This script will build out a sample DMZ setup containing:
   - A default storage account for VM disks
   - Two new cloud services
   - Two Subnets (FrontEnd and BackEnd subnets)
   - One server on hello FrontEnd Subnet
   - Three Servers on hello BackEnd Subnet
   - Network Security Groups tooallow/deny traffic patterns as declared

  Before running script, ensure hello network configuration file is created in
  hello directory referenced by $NetworkConfigFile variable (or update the
  variable tooreflect hello path and file name of hello config file being used).

 .Notes
  Security requirements are different for each use case and can be addressed in a
  myriad of ways. Please be sure that any sensitive data or applications are behind
  hello appropriate layer(s) of protection. This script serves as an example of some
  of hello techniques that can be used, but should not be used for all scenarios. You
  are responsible tooassess your security needs and hello appropriate protections
  needed, and then effectively implement those protections.

  FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
   IIS01      - 10.0.1.5

  BackEnd Service (BackEnd subnet 10.0.2.0/24)
   DNS01      - 10.0.2.4
   AppVM01    - 10.0.2.5
   AppVM02    - 10.0.2.6

#>

# Fixed Variables
    $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password toobe used for all VMs"
    $VMName = @()
    $ServiceName = @()
    $VMFamily = @()
    $img = @()
    $size = @()
    $SubnetName = @()
    $VMIP = @()

# User-Defined Global Variables
  # These should be changes tooreflect your subscription and services
  # Invalid options will fail in hello validation section

  # Subscription Access Details
    $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

  # VM Account, Location, and Storage Details
    $LocalAdmin = "theAdmin"
    $DeploymentLocation = "Central US"
    $StorageAccountName = "vmstore02"

  # Service Details
    $FrontEndService = "FrontEnd001"
    $BackEndService = "BackEnd001"

  # Network Details
    $VNetName = "CorpNetwork"
    $FESubnet = "FrontEnd"
    $FEPrefix = "10.0.1.0/24"
    $BESubnet = "BackEnd"
    $BEPrefix = "10.0.2.0/24"
    $NetworkConfigFile = "C:\Scripts\NetworkConf1.xml"

  # VM Base Disk Image Details
    $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

  # NSG Details
    $NSGName = "MyVNetSG"

# User-Defined VM Specific Configuration
    # Note: tooensure proper NSG Rule creation later in this script:
    #       - hello Web Server must be VM 0
    #       - hello AppVM1 Server must be VM 1
    #       - hello DNS server must be VM 3
    #
    #       Otherwise hello NSG rules in hello last section of this
    #       script will need toobe changed toomatch hello modified
    #       VM array numbers ($i) so hello NSG Rule IP addresses
    #       are aligned toohello associated VM IP addresses.

    # VM 0 - hello Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - hello First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - hello Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - hello DNS Server
      $VMName += "DNS01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.4"

# ----------------------------- #
# No User-Defined Variables or  #
# Configuration past this point #
# ----------------------------- #    

  # Get your Azure accounts
    Add-AzureAccount
    Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
    Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

  # Create Storage Account
    If (Test-AzureName -Storage -Name $StorageAccountName) { 
        Write-Host "Fatal Error: This storage account name is already in use, please pick a different name." -ForegroundColor Red
        Return}
    Else {Write-Host "Creating Storage Account" -ForegroundColor Cyan 
          New-AzureStorageAccount -Location $DeploymentLocation -StorageAccountName $StorageAccountName}

  # Update Subscription Pointer tooNew Storage Account
    Write-Host "Updating Subscription Pointer tooNew Storage Account" -ForegroundColor Cyan 
    Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

# Validation
$FatalError = $false

If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
     Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
     $FatalError = $true}

If (Test-AzureName -Service -Name $FrontEndService) { 
    Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

If (Test-AzureName -Service -Name $BackEndService) { 
    Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

If (-Not (Test-Path $NetworkConfigFile)) { 
    Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation variable is correct and hello network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see hello above messages for more information." -ForegroundColor Red
    Return}
Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

# Create VNET
    Write-Host "Creating VNET" -ForegroundColor Cyan 
    Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

# Create Services
    Write-Host "Creating Services" -ForegroundColor Cyan
    New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
    New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

# Build VMs
    $i=0
    $VMName | Foreach {
        Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
        New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
            Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
            Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
            Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
            Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
            Remove-AzureEndpoint -Name "PowerShell" | `
            New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
            # Note: A Remote Desktop endpoint is automatically created when each VM is created.
        $i++
    }
    # Add HTTP Endpoint for IIS01
    Get-AzureVM -ServiceName $ServiceName[0] -Name $VMName[0] | Add-AzureEndpoint -Name HTTP -Protocol tcp -LocalPort 80 -PublicPort 80 | Update-AzureVM

# Configure NSG
    Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

  # Build hello NSG
    Write-Host "Building hello NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) too$($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
        -Protocol *

    # Assign hello NSG toohello Subnets
        Write-Host "Binding hello NSG tooboth subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

# Optional Post-script Manual Configuration
  # Install Test Web App (Run Post-Build Script on hello IIS Server)
  # Install Backend resource (Run Post-Build Script on hello AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a>Archivo de configuración de red
Guarde este archivo xml con la ubicación actualizada y agregue variable de hello link toothis archivo toohello $NetworkConfigFile Hola anterior secuencia de comandos.

```XML
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
  <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="DNS01" IPAddress="10.0.2.4" />
        <DnsServer name="Level3" IPAddress="209.244.0.3" />
      </DnsServers>
    </Dns>
    <VirtualNetworkSites>
      <VirtualNetworkSite name="CorpNetwork" Location="Central US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="FrontEnd">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="BackEnd">
            <AddressPrefix>10.0.2.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
        <DnsServersRef>
          <DnsServerRef name="DNS01" />
          <DnsServerRef name="Level3" />
        </DnsServersRef>
      </VirtualNetworkSite>
    </VirtualNetworkSites>
  </VirtualNetworkConfiguration>
</NetworkConfiguration>
```

#### <a name="sample-application-scripts"></a>Scripts de aplicación de ejemplo
Si desea tooinstall una aplicación de ejemplo para este y otros ejemplos de la red Perimetral, se aplicó en hello siguiente vínculo: [Script de aplicación de ejemplo][SampleApp]

## <a name="next-steps"></a>Pasos siguientes
* Actualice y guarde el archivo XML.
* Ejecute hello PowerShell script toobuild Hola entorno
* Instalar la aplicación de ejemplo de Hola
* Probar los flujos de tráfico distintos a través de esta red perimetral

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "Red perimetral de entrada con grupo de seguridad de red"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

