---
title: 'aaaDMZ ejemplo: crear una red Perimetral tooprotect aplicaciones con un Firewall y los NSG | Documentos de Microsoft'
description: "Creación de una red perimetral con un firewall y grupos de seguridad de red (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: c78491c7-54ac-4469-851c-b35bfed0f528
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: 18f116dc3897567bff14a509ae8c13f449182bfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="example-2--build-a-dmz-tooprotect-applications-with-a-firewall-and-nsgs"></a>Ejemplo 2: crear una red Perimetral tooprotect aplicaciones con un Firewall y los NSG
[Devolver toohello página de prácticas recomendadas de seguridad límite][HOME]

En este ejemplo se creará una red perimetral con un firewall, cuatro servidores Windows y grupos de seguridad de red. También guiará a través de cada uno de los tooprovide de comandos pertinentes de hello una comprensión más profunda de cada paso. También hay un escenario de tráfico sección tooprovide una detallada paso a paso cómo tráfico pasa a través de las capas de defensa en Hola Hola red Perimetral. Por último, en la sección de referencias de hello es código completo de Hola e instrucción toobuild este entorno tootest y experimentar con diferentes escenarios. 

![Entrada de la red Perimetral con NVA y NSG][1]

## <a name="environment-description"></a>Descripción del entorno
En este ejemplo hay una suscripción que contiene Hola siguiente:

* Dos servicios en la nube: "FrontEnd001" y "BackEnd001"
* Una red virtual, CorpNetwork, con dos subredes: FrontEnd y BackEnd
* Un único grupo de seguridad de red que está aplicada tooboth subredes
* Un dispositivo de red virtual, en este ejemplo, un NextGen Firewall Barracuda, conectado toohello subred de front-end
* Un servidor Windows que representa un servidor de aplicaciones web ("IIS01")
* Dos servidores Windows que representan servidores back-end de aplicaciones (“AppVM01”, “AppVM02”)
* Un servidor Windows que representa un servidor DNS ("DNS01")

> [!NOTE]
> Aunque en este ejemplo usa un NextGen Firewall Barracuda, muchos de los diferentes dispositivos de red Virtual podría utilizarse para este ejemplo de Hola.
> 
> 

En la sección de referencias de Hola a continuación hay un script de PowerShell que se compilará la mayor parte del entorno de Hola que se ha descrito anteriormente. Hola de crear las máquinas virtuales y redes virtuales, aunque se realizan mediante el script de ejemplo de Hola, no se describen en detalle en este documento.

entorno de Hola toobuild:

1. Guardar archivo de xml de configuración Hola red incluido en la sección de referencias de hello (actualizada con nombres, la ubicación y el escenario de hello dada de toomatch de direcciones IP)
2. Variables de usuario de actualización hello en hello toomatch Hola entorno Hola de script es toobe ejecutarán (suscripciones, los nombres de servicio, etcetera)
3. Ejecutar script de Hola en PowerShell

**Tenga en cuenta**: región Hola indicado en el script de PowerShell de hello debe coincidir con la región Hola indicado en el archivo de xml de configuración de red de Hola.

Una vez que el script de Hola se ejecuta correctamente puede tener Hola siguiendo los pasos posteriores a la secuencia de comandos:

1. Configurar reglas de firewall de hello, este tema se trata en la sección de hello siguiente titulada: las reglas de Firewall.
2. Opcionalmente, en la sección de referencias de hello son dos tooset de secuencias de comandos de hello web y servidor de aplicaciones con una tooallow de aplicación web simple pruebas con esta configuración de red Perimetral.

Hola próxima sección explica la mayoría de las secuencias de comandos de hello instrucciones relativa tooNetwork grupos de seguridad.

## <a name="network-security-groups-nsg"></a>Grupos de seguridad de red (NSG)
En este ejemplo, se crea un grupo de grupos de seguridad de red y después se carga con seis reglas. 

> [!TIP]
> Por lo general, debe crear primero las reglas específicas de "Permitir" y, a continuación, Hola reglas más genéricas de "Denegar" última. Hola tenga asignada la prioridad determina qué reglas se evalúan primero. Una vez que el tráfico se encuentra la regla específica de tooapply tooa, no se evalúa ninguna otra regla. Se pueden aplicar reglas NSG en la vista en hello dirección entrante o saliente (desde la perspectiva de Hola de subred de hello).
> 
> 

Mediante declaración, se regeneran Hola siguiendo las reglas para el tráfico entrante:

1. Se permite el tráfico DNS interno (puerto 53)
2. Se permite el tráfico RDP (puerto 3389) de hello Internet tooany VM
3. Se permite el tráfico HTTP (puerto 80) de hello Internet toohello NVA (firewall)
4. Se permite cualquier tráfico (todos los puertos) del IIS01 tooAppVM1
5. Todo (todos los puertos) el tráfico de hello Internet toohello se deniega todo red virtual (tanto en las subredes)
6. Se deniega todo (todos los puertos) el tráfico de subred de back-end de hello front-end subred toohello

Con estas subredes de enlazado tooeach reglas, si una solicitud HTTP es entrante desde el servidor web de hello Internet toohello, ambas reglas 3 (permitir) y 5 (denegar) aplicaría, pero dado que la regla 3 tiene mayor prioridad solo aplicaría y regla 5 podría no entran en juego. Por lo tanto solicitud Hola HTTP podría permitirse toohello firewall. Si ese mismo tráfico estaba intentando server DNS01 de tooreach hello, regla 5 (Deny) sería Hola primera hello y tooapply el tráfico no estarían permitido a toopass toohello server. Regla 6 (Deny) bloques Hola front-end de subred hablando de la subred de back-end de toohello (excepto el tráfico permitido en las reglas 1 y 4), esto protege la red de back-end de hello en caso de que un atacante pone en peligro hello web aplicación en hello front-end, tendría atacante Hola acceso limitado toohello back-end "protegido" red (solo tooresources expuesta en el servidor de hello AppVM01).

Hay una regla de salida predeterminada que permite el tráfico de salida toohello internet. En este ejemplo, permitimos el tráfico saliente y no modificamos las reglas de salida. toolock hacia abajo el tráfico en ambas direcciones, enrutamiento de definido por usuario es obligatorio, esto se explora en otro ejemplo que puede encontrar en hello [documento de límite de seguridad principal][HOME].

las reglas NSG de Hello anterior descrito son reglas NSG toohello muy similares en [ejemplo 1: crear una red Perimetral Simple con NSG][Example1]. Revise hello NSG descripción en ese documento para una visión detallada de cada regla NSG y sus atributos.

## <a name="firewall-rules"></a>Reglas de firewall
Un cliente de administración deberá toobe instalado en un servidor de seguridad de PC toomanage hello y crear configuraciones de hello necesarias. Vea proveedor de documentación de su firewall (o en otro NVA) hello en cómo toomanage Hola dispositivo. resto Hola de esta sección describe la configuración Hola de firewall de hello, a través del cliente de administración de proveedores de hello (es decir, no Hola portal de Azure o PowerShell).

Instrucciones para la descarga de cliente y conexión toohello Barracuda utilizado en este ejemplo pueden encontrarse aquí: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)

En firewall de hello, las reglas de reenvío debe toobe creado. Dado que este ejemplo solo enruta el tráfico de entrada toohello firewall de internet y, a continuación, el servidor de web de toohello, se necesita reenvío solo una regla NAT. En hello Barracuda NextGen Firewall utilizado en este Hola ejemplo regla sería una NAT de destino de regla "(Dst" NAT) toopass este tráfico.

siguiente de hello toocreate regla (o comprobar las reglas existentes de forma predeterminada), a partir de panel de cliente de administración de dispositivo Barracuda NG hello, vaya la ficha de configuración de toohello, Hola configuración operativa sección, haga clic en el conjunto de reglas. Llama a una cuadrícula, "Main reglas" mostrará Hola existente las reglas activas y desactivadas en firewall de Hola. En hello superior derecha de esta cuadrícula es una pequeña, de color verde "+" botón, haga clic en este toocreate una nueva regla (Nota: el firewall puede "bloquear" para los cambios, si ve un botón de marca "Bloquear" y son no se puede toocreate o editar las reglas, haga clic en este botón demasiado "desbloquear" hello conjunto de reglas y permitir la edición). Si desea tooedit una regla existente, seleccione esa regla, haga clic en y seleccione Editar regla.

Cree una nueva regla y asígnele un nombre, como "WebTraffic". 

icono de regla de NAT de destino de Hello tiene el siguiente aspecto: ![icono de NAT de destino][2]

regla de Hello propio sería algo parecido a esto:

![Regla de Firewall][3]

Aquí cualquier dirección entrante que aciertos Hola Firewall intentar tooreach HTTP (puerto 80 o 443 para HTTPS) se enviarán Hola interfaz "DHCP1 Local IP" del Firewall y redirigida toohello servidor Web con la dirección IP de 10.0.1.5 Hola. Dado que el tráfico de hello próximas novedades en el puerto 80 en y en curso toohello web en el puerto 80 no se necesita ningún cambio de puerto. Sin embargo, Hola lista de destino podrían haber resultado 10.0.1.5:8080 si el servidor Web escucha en el puerto 8080, por tanto, traducir Hola entrante del puerto 80 en hello firewall tooinbound puerto 8080 Hola servidor web.

Un método de conexión debe también ser indicado, para hello la regla de destino de hello Internet, "Dinámica SNAT" es el más adecuado. 

Aunque se creó una regla, es importante que su prioridad se establezca correctamente. Si en la cuadrícula de Hola de todas las reglas de firewall de hello que esta nueva regla se encuentra en parte inferior de hello (debajo de la regla de "BLOCKALL" hello) nunca se entran en juego. Asegúrese de regla Hola recién creada para el tráfico web está por encima de la regla BLOCKALL Hola.

Una vez que se crea la regla de hello, debe insertar toohello firewall y, a continuación, activar, si no es así regla Hola cambios no surtirán efecto. proceso de activación e inserción de Hola se describe en la sección siguiente Hola.

## <a name="rule-activation"></a>Activación de reglas
Con hello ruleset modifica tooadd esta regla, debe ser Hola ruleset cargado toohello firewall y activado.

![Activación de reglas de firewall][4]

En la esquina superior derecha de Hola de cliente de administración de hello son un clúster de botones. Haga clic en firewall de Hola "enviar cambios" botón toosend Hola modificar reglas toohello, a continuación, haga clic en el botón de "Activar" Hola.

Con la activación de Hola de conjunto de reglas de firewall de hello esta compilación de entorno de ejemplo está completa. Si lo desea, scripts de compilación de post Hola Hola referencias sección puede ser ejecutan tooadd una aplicación toothis entorno tootest hello por debajo de los escenarios de tráfico.

> [!IMPORTANT]
> Es toorealize crítico que no alcanzará a servidor web de hello directamente. Cuando un explorador solicita una página HTTP desde FrontEnd001.CloudApp.Net, pasadas de hello HTTP (puerto 80) del punto de conexión no Hola este tráfico toohello firewall del servidor web. Hola firewall a continuación, según la regla de toohello creado anteriormente, NAT que solicitan toohello servidor Web.
> 
> 

## <a name="traffic-scenarios"></a>Escenarios de tráfico
#### <a name="allowed-web-tooweb-server-through-firewall"></a>(Permitido) TooWeb Web Server a través del Firewall
1. El usuario de Internet solicita la página HTTP desde FrontEnd001.CloudApp.Net (servicio en la nube accesible desde Internet).
2. Fases de tráfico del servicio de nube a través de un extremo abierto en la interfaz local de toofirewall el puerto 80 en 10.0.1.4:80
3. La subred front-end comienza el procesamiento de las reglas de entrada:
   1. 1 de la regla de NSG (DNS) no se aplica, mover toonext regla
   2. 2 de la regla de NSG (RDP) no se aplica, mover toonext regla
   3. Aplicar NSG regla 3 (tooFirewall Internet), el tráfico es el procesamiento de reglas permitidas, detenga
4. Tráfico llega a dirección IP interna del servidor de seguridad de hello (10.0.1.4)
5. Regla de reenvío de Firewall vea esto es tráfico en el puerto 80, se redirige el servidor web de toohello IIS01
6. Iis01 escucha el tráfico de web, recibe esta solicitud y comienza a procesar la solicitud de Hola
7. Iis01 pide Hola SQL Server en AppVM01 información
8. No hay reglas de salida en la subred front-end, se permite el tráfico.
9. subred de back-end de Hello comienza el procesamiento de la regla de entrada:
   1. 1 de la regla de NSG (DNS) no se aplica, mover toonext regla
   2. 2 de la regla de NSG (RDP) no se aplica, mover toonext regla
   3. Regla de NSG 3 (tooFirewall Internet) no se aplica, mover toonext regla
   4. Aplicar NSG regla 4 (IIS01 tooAppVM01), el tráfico es el procesamiento de reglas permitidas, detenga
10. AppVM01 recibe Hola consulta SQL y responde
11. Puesto que no hay ninguna regla de salida en hello respuesta de Hola de subred de back-end se permite
12. La subred front-end comienza el procesamiento de las reglas de entrada:
    1. No hay ninguna regla NSG que se aplica tooInbound tráfico de subred de front-end del toohello Hola de subred de back-end, por lo que no se aplica ninguno de reglas NSG Hola
    2. Hola regla predeterminada del sistema permitiendo el tráfico entre subredes permitiría este tráfico, por lo que se permite el tráfico de Hola.
13. servidor IIS de Hello recibe la respuesta SQL de Hola y completa respuesta HTTP de Hola y envía toohello solicitante
14. Puesto que se trata de una sesión NAT de firewall de hello, destino de la respuesta de hello (inicialmente) es para hello Firewall
15. firewall de Hello recibe respuesta Hola Hola servidor Web y reenvía toohello back-usuario de Internet
16. Dado que hay no se permite ninguna regla de salida en respuesta de Hola de subred de front-end de Hola y Hola usuario de Internet recibe hello web página solicitada.

#### <a name="allowed-rdp-toobackend"></a>(Permitido) TooBackend RDP
1. Administrador del servidor en internet solicita tooAppVM01 de sesión RDP en BackEnd001.CloudApp.Net:xxxxx donde xxxxx es el número de puerto de hello asignada aleatoriamente para tooAppVM01 RDP (puerto Hola asignado se puede encontrar en hello Portal de Azure o a través de PowerShell)
2. Desde Hola que Firewall sólo está escuchando en hello FrontEnd001.CloudApp.Net dirección no está implicado en este flujo de tráfico
3. La subred back-end comienza el procesamiento de las reglas de entrada:
   1. 1 de la regla de NSG (DNS) no se aplica, mover toonext regla
   2. Se aplica la regla 2 (RDP) de grupo de seguridad de red, se permite el tráfico, detener el procesamiento de las reglas.
4. No hay reglas de salida, se aplican las reglas predeterminadas y se permite el tráfico de retorno.
5. La sesión RDP está habilitada.
6. AppVM01 solicita la contraseña del nombre de usuario.

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a>(Permitido) Búsqueda de DNS del servidor web en el servidor DNS
1. Web necesidades de servidor, IIS01, fuente de distribución de datos en www.data.gov, pero necesita tooresolve Hola dirección.
2. Hola configuración de red para las listas de red virtual de hello DNS01 (10.0.2.4 de subred de back-end de hello) como servidor DNS principal de hello, IIS01 envía Hola DNS solicitud tooDNS01
3. No hay reglas de salida en la subred front-end, se permite el tráfico.
4. La subred back-end comienza el procesamiento de las reglas de entrada:
   1. Se aplica la regla 1 (DNS) de grupo de seguridad de red, se permite el tráfico, detener el procesamiento de las reglas.
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

#### <a name="allowed-web-server-access-file-on-appvm01"></a>(Permitido) Archivo de acceso del servidor web en AppVM01
1. IIS01 solicita un archivo en AppVM01
2. No hay reglas de salida en la subred front-end, se permite el tráfico.
3. subred de back-end de Hello comienza el procesamiento de la regla de entrada:
   1. 1 de la regla de NSG (DNS) no se aplica, mover toonext regla
   2. 2 de la regla de NSG (RDP) no se aplica, mover toonext regla
   3. Regla de NSG 3 (tooFirewall Internet) no se aplica, mover toonext regla
   4. Aplicar NSG regla 4 (IIS01 tooAppVM01), el tráfico es el procesamiento de reglas permitidas, detenga
4. AppVM01 recibe la solicitud de Hola y responde con el archivo (suponiendo que se autoriza el acceso)
5. Puesto que no hay ninguna regla de salida en hello respuesta de Hola de subred de back-end se permite
6. La subred front-end comienza el procesamiento de las reglas de entrada:
   1. No hay ninguna regla NSG que se aplica tooInbound tráfico de subred de front-end del toohello Hola de subred de back-end, por lo que no se aplica ninguno de reglas NSG Hola
   2. Hola regla predeterminada del sistema permitiendo el tráfico entre subredes permitiría este tráfico, por lo que se permite el tráfico de Hola.
7. servidor IIS de Hello recibe el archivo hello

#### <a name="denied-web-direct-tooweb-server"></a>(Denegado) TooWeb directo de Web Server
Desde hello Firewall, IIS01 y Hola servidor Web están en hello mismo servicio en la nube comparten Hola misma dirección IP pública. Por lo tanto se dirigirá todo el tráfico HTTP toohello firewall. Mientras que resultará usar correctamente la solicitud de hello, no se puede ir directamente a toohello servidor Web, pasa, según lo previsto, a través de Hola de Firewall en primer lugar. Vea Hola primer escenario de esta sección para el flujo de tráfico de Hola.

#### <a name="denied-web-toobackend-server"></a>(Denegado) TooBackend Web Server
1. Usuario de Internet intenta tooaccess un archivo en AppVM01 a través de hello BackEnd001.CloudApp.Net servicio
2. Dado que no hay ningún extremo abierto para el recurso compartido de archivos, esto no sucedería Hola servicio en la nube y no llegar a servidor hello
3. Si los puntos de conexión de hello estaban abiertos por algún motivo, la regla de NSG 5 (Internet tooVNet) bloquearían este tráfico

#### <a name="denied-web-dns-lookup-on-dns-server"></a>(Denegado) Búsqueda de DNS web en el servidor DNS
1. Usuario de Internet intenta toolookup un registro DNS interno en DNS01 a través de hello BackEnd001.CloudApp.Net servicio
2. Dado que no hay ningún extremo abierto para DNS, esto no pasaría Hola servicio en la nube y no llegar a servidor hello
3. Si los puntos de conexión de hello estaban abiertos por algún motivo, la regla de NSG 5 (Internet tooVNet) bloquearían este tráfico (Nota: esa regla 1 (DNS) no se aplicarían por dos motivos, primera dirección de origen de hello es Hola internet, esta regla solo aplica toohello red virtual local como Hola de origen, también se trata de una regla de permiso, por lo que nunca podría denegar el tráfico)

#### <a name="denied-web-toosql-access-through-firewall"></a>(Denegado) Acceso Web de tooSQL a través del Firewall
1. El usuario de Internet solicita los datos SQL desde FrontEnd001.CloudApp.Net (servicio en la nube accesible desde Internet).
2. Dado que no hay ningún extremo abierto para SQL, esto no sucedería Hola servicio en la nube y no llegar a firewall de Hola
3. Si los puntos de conexión estaban abiertos por algún motivo, subred de front-end de hello comienza el procesamiento de la regla de entrada:
   1. 1 de la regla de NSG (DNS) no se aplica, mover toonext regla
   2. 2 de la regla de NSG (RDP) no se aplica, mover toonext regla
   3. Aplicar NSG regla 2 (tooFirewall Internet), el tráfico es el procesamiento de reglas permitidas, detenga
4. Tráfico llega a dirección IP interna del servidor de seguridad de hello (10.0.1.4)
5. Servidor de seguridad no tiene ninguna regla de reenvío para SQL y quita Hola tráfico

## <a name="conclusion"></a>Conclusión
Se trata de una manera relativamente sencillo de protección de su aplicación con un firewall y el aislamiento de la subred de back-end de Hola de tráfico entrante.

Puede encontrar más ejemplos y una descripción general de los límites de seguridad de red [aquí][HOME].

## <a name="references"></a>Referencias
### <a name="main-script-and-network-config"></a>Script principal y configuración de red
Guardar Hola Script completo en un archivo de script de PowerShell. Guardar configuración de red de hello en un archivo denominado "NetworkConf2.xml".
Modifique las variables definidas por el usuario de hello según sea necesario. Ejecutar script de Hola, a continuación, siga anterior de instrucciones de instalación del regla de Firewall Hola.

#### <a name="full-script"></a>Script completo
Este script superará en función de las variables definidas por el usuario de hello:

1. Conectar tooan suscripción de Azure
2. Creación de una cuenta de almacenamiento nueva
3. Crear una red virtual nueva y dos subredes tal como se define en el archivo de configuración de red de Hola
4. Creación de cuatro máquinas virtuales de servidor Windows
5. Configuración del grupo de seguridad de red, incluido lo siguiente:
   * Creación de un grupo de seguridad de red
   * Rellenado con reglas
   * Enlace hello NSG toohello las subredes correspondientes

Este script de PowerShell debe ejecutarse localmente en un equipo o servidor conectado a Internet.

> [!IMPORTANT]
> Cuando se ejecuta este script, puede haber advertencias u otros mensajes informativos que se muestran en PowerShell. Solo los mensajes de error indicados en rojo son motivo de preocupación.
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and Network Security Groups in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Two new cloud services
       - Two Subnets (FrontEnd and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet (plus hello NVA on hello FrontEnd subnet)
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
       myFirewall - 10.0.1.4
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

    # User Defined Global Variables
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
        $NetworkConfigFile = "C:\Scripts\NetworkConf2.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure proper NSG Rule creation later in this script:
        #       - hello Web Server must be VM 1
        #       - hello AppVM1 Server must be VM 2
        #       - hello DNS server must be VM 4
        #
        #       Otherwise hello NSG rules in hello last section of this
        #       script will need toobe changed toomatch hello modified
        #       VM array numbers ($i) so hello NSG Rule IP addresses
        #       are aligned toohello associated VM IP addresses.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $FrontEndService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.5"

        # VM 2 - hello First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - hello Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - hello DNS Server
          $VMName += "DNS01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.4"

    # ----------------------------- #
    # No User Defined Varibles or   #
    # Configuration past this point #
    # ----------------------------- #

      # Get your Azure accounts
        Add-AzureAccount
        Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
        Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

      # Create Storage Account
        If (Test-AzureName -Storage -Name $StorageAccountName) { 
            Write-Host "Fatal Error: This storage account name is already in use, please pick a diffrent name." -ForegroundColor Red
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
    Else { Write-Host "hello network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation varible is correct and hello netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see hello above messages for more information." -ForegroundColor Red
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
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all hello EndPoints we'll need once we're up and running
                # Note: Web traffic goes through hello firewall, so we'll need tooset up a HTTP endpoint.
                #       Also, hello firewall will be redirecting web traffic tooa new IP and Port in a
                #       forwarding rule, so hello HTTP endpoint here will have hello same public and local
                #       port and hello firewall will do hello NATing and redirection as declared in the
                #       firewall rule.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                    # Note: A Remote Desktop endpoint is automatically created when each VM is created.
                }
            $i++
        }

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rules
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
            -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[4] -DestinationPortRange '53' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
            -SourceAddressPrefix Internet -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[1]) too$($VMName[2])" -Type Inbound -Priority 130 -Action Allow `
            -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[2] -DestinationPortRange '*' `
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
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on hello IIS Server)
      # Install Backend resource (Run Post-Build Script on hello AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a>Archivo de configuración de red
Guarde este archivo xml con la ubicación actualizada y agregue Hola vínculo toothis toohello $NetworkConfigFile variable de archivos de script de Hola anterior.

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

#### <a name="sample-application-scripts"></a>Scripts de aplicación de ejemplo
Si desea tooinstall una aplicación de ejemplo para este y otros ejemplos de la red Perimetral, se aplicó en hello siguiente vínculo: [Script de aplicación de ejemplo][SampleApp]

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "Red perimetral de entrada con grupo de seguridad de red"
[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "Icono de NAT de destino"
[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "Regla de firewall"
[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "Activación de reglas de firewall"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
[Example1]: ./virtual-networks-dmz-nsg-asm.md
