---
title: 'aaaDMZ ejemplo: crear una red Perimetral tooProtect redes con un Firewall, UDR y NSG | Documentos de Microsoft'
description: "Creación de una red perimetral con un firewall, enrutamiento definido por el usuario (UDR) y grupos de seguridad de red (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: dc01ccfb-27b0-4887-8f0b-2792f770ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: cc121f9cd5fe3c3e9ac2c70fbb7d982a80bb345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="example-3--build-a-dmz-tooprotect-networks-with-a-firewall-udr-and-nsg"></a>Ejemplo 3: crear una red Perimetral tooProtect redes con un Firewall, UDR y NSG
[Devolver toohello página de prácticas recomendadas de seguridad límite][HOME]

En este ejemplo se creará una red perimetral con un firewall, cuatro servidores Windows, enrutamiento definido por el usuario y grupos de seguridad de red. También guiará a través de cada uno de los tooprovide de comandos pertinentes de hello una comprensión más profunda de cada paso. También hay un escenario de tráfico sección tooprovide una detallada paso a paso cómo tráfico pasa a través de las capas de defensa en Hola Hola red Perimetral. Por último, en la sección de referencias de hello es código completo de Hola e instrucción toobuild este entorno tootest y experimentar con diferentes escenarios. 

![Red perimetral bidireccional con un dispositivo de red virtual, grupos de seguridad de red y enrutamiento definido por el usuario][1]

## <a name="environment-setup"></a>Configuración del entorno
En este ejemplo hay una suscripción que contiene Hola siguiente:

* Tres servicios en la nube: “SecSvc001”, “FrontEnd001” y “BackEnd001”
* Una red virtual, CorpNetwork, con tres subredes: SecNet, FrontEnd y BackEnd
* Un dispositivo de red virtual, en este ejemplo, un firewall, conectado toohello SecNet subred
* Un servidor Windows que representa un servidor de aplicaciones web ("IIS01")
* Dos servidores Windows que representan servidores back-end de aplicaciones (“AppVM01”, “AppVM02”)
* Un servidor Windows que representa un servidor DNS ("DNS01")

En la sección de referencias de Hola a continuación hay un script de PowerShell que se compilará la mayor parte del entorno de Hola que se ha descrito anteriormente. Hola de crear las máquinas virtuales y redes virtuales, aunque se realizan mediante el script de ejemplo de Hola, no se describen en detalle en este documento.

entorno de Hola toobuild:

1. Guardar archivo de xml de configuración Hola red incluido en la sección de referencias de hello (actualizada con nombres, la ubicación y el escenario de hello dada de toomatch de direcciones IP)
2. Variables de usuario de actualización hello en hello toomatch Hola entorno Hola de script es toobe ejecutarán (suscripciones, los nombres de servicio, etcetera)
3. Ejecutar script de Hola en PowerShell

**Tenga en cuenta**: región Hola indicado en el script de PowerShell de hello debe coincidir con la región Hola indicado en el archivo de xml de configuración de red de Hola.

Una vez que el script de Hola se ejecuta correctamente puede tener Hola siguiendo los pasos posteriores a la secuencia de comandos:

1. Configurar reglas de firewall de hello, este tema se trata en la sección de hello siguiente titulada: descripción de la regla de Firewall.
2. Opcionalmente, en la sección de referencias de hello son dos tooset de secuencias de comandos de hello web y servidor de aplicaciones con una tooallow de aplicación web simple pruebas con esta configuración de red Perimetral.

Una vez que el script de Hola se ejecuta correctamente las reglas de firewall de hello necesitarán toobe completado, este tema se trata en la sección de hello: las reglas de Firewall.

## <a name="user-defined-routing-udr"></a>Enrutamiento definido por el usuario (UDR)
De forma predeterminada, Hola siguiendo las rutas del sistema se define como:

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

Hola VNETLocal siempre es Hola definido dirección prefix(es) de hello red virtual para dicha red específica (es decir dejará de red virtual tooVNet dependiendo de cómo se defina cada red virtual específica). rutas de sistema de Hello restantes son estáticas y predeterminado como anteriormente.

Como prioridad, las rutas se procesan a través del método de coincidencia de prefijo más largo (LPM) hello, así hello ruta más específica en la tabla de hello aplicaría tooa partir de dirección de destino.

Por lo tanto, se enrutaría tráfico (por ejemplo toohello DNS01 server, 10.0.2.4) que se usa para la red local de hello (10.0.0.0/16) a través de destino de tooits de red virtual de hello debido toohello 10.0.0.0/16 ruta. En otras palabras, para 10.0.2.4, ruta de hello 10.0.0.0/16 es ruta más específica de hello, aunque 0.0.0.0/0 y Hola 10.0.0.0/8 también pudieron aplicar, pero ya que son menos específicos no afectan a este tráfico. Por lo tanto Hola tráfico too10.0.2.4 tendría un próximo salto de Hola red virtual local y simplemente enrutar toohello destino.

Si el tráfico se ha diseñado para 10.1.1.1 por ejemplo, no aplica la ruta de hello 10.0.0.0/16, pero Hola 10.0.0.0/8 sería hello más específica, y este tráfico Hola sería quitar ("negro holed"), ya que Hola próximo salto es Null. 

Si destino hello no aplica tooany de prefijos de Null de Hola o prefijos de VNETLocal hello, seguiría Hola menos específica enrutar, 0.0.0.0/0 y enrutarse toohello Internet como próximo salto de hello y, por tanto, out perimetral de internet de Azure.

Si hay dos prefijos idénticos en la tabla de rutas de hello, Hola aquí te mostramos orden Hola de preferencia en función de atributo de "origen" de las rutas de hello:

1. "VirtualAppliance" = una tabla de agregados manualmente toohello ruta definida por el usuario
2. "VPNGateway" = una ruta dinámicos BGP (cuando se usa con las redes híbridas), agrega un protocolo de red dinámica, estas rutas pueden cambiar con el tiempo como protocolo de dinámica de hello automáticamente refleja los cambios de red emparejar
3. "Default" = Hola sistema rutas, Hola entradas estáticas de hello y red virtual locales tal y como se muestra en la tabla de rutas de hello anterior.

> [!NOTE]
> Ahora puede usar enrutamiento definido por usuario (UDR) con ExpressRoute y puertas de enlace VPN tooforce saliente y entrantes entre entornos tráfico toobe tooa enrutado virtual otros dispositivos de red (NVA).
> 
> 

#### <a name="creating-hello-local-routes"></a>Creación de hello las rutas locales
En este ejemplo, se necesitan dos tablas de enrutamiento, uno para las subredes de front-end y back-end de Hola. Cada tabla se carga con rutas estáticas adecuadas para hello dada la subred. A fin de Hola de este ejemplo, cada tabla tiene tres rutas:

1. Tráfico de subred local con ningún servidor de seguridad de próximo salto define tooallow subred local tráfico toobypass Hola
2. Tráfico de red virtual con un próximo salto definido como firewall, se invalida la regla predeterminada de Hola que permite tooroute de tráfico de red virtual local directamente
3. Tráfico todas las restante (0/0) con un próximo salto se define como Hola firewall

Una vez creadas las tablas de enrutamiento de hello son subredes tootheir enlazado. Para la tabla de enrutamiento de hello front-end subred, una vez que crea y enlaza toohello subred debe ser similar a:

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active 
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active


En este ejemplo, siguiente Hola comandos son toobuild usa una tabla de rutas hello, agregue una ruta definida por el usuario y, a continuación, enlazar la subred de tooa de tabla de ruta de hello (tenga en cuenta; los elementos situados debajo de la que comienza con un signo de dólar (p. ej.: $BESubnet) son variables definidas por el usuario desde un script de Hola en sección de referencia de Hola de este documento):

1. Se debe crear la primera Hola base tabla de enrutamiento. Este fragmento de código muestra la creación de hello de tabla de hello para la subred de back-end de Hola. En el script de Hola, también se crea una tabla correspondiente para la subred de front-end de Hola.
   
     New-AzureRouteTable -Name $BERouteTableName `
   
         -Location $DeploymentLocation `
         -Label "Route table for $BESubnet subnet"
2. Una vez que se crea la tabla de rutas de hello, se pueden agregar rutas definidas por el usuario específico. En este fragmento, se enrutará todo el tráfico (0.0.0.0/0) a través del dispositivo virtual de hello (una variable, $VMIP [0] es toopass usado en la dirección IP de hello asignada al dispositivo virtual Hola se creó anteriormente en el script de Hola). En el script de Hola, también se crea una regla correspondiente en la tabla de front-end de Hola.
   
     Get-AzureRouteTable $BERouteTableName | `
   
         Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
         -NextHopType VirtualAppliance `
         -NextHopIpAddress $VMIP[0]
3. Hola por encima de las entradas de ruta invalidará ruta de hello predeterminada "0.0.0.0/0", pero regla 10.0.0.0/16 Hola predeterminada que aún existen de forma que permitiría tráfico dentro de tooroute de red virtual de hello directamente toohello destino y no toohello dispositivo de red Virtual. toocorrect que se debe agregar esta regla de seguimiento de Hola de comportamiento.
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
4. En este momento no hay un toobe elección realizado. Con hello por encima de dos rutas todo el tráfico enrutará toohello firewall para evaluación, incluso el tráfico dentro de una sola subred. Esto puede ser deseable, pero tooallow tráfico dentro de un tooroute de subred localmente sin la participación del firewall de Hola se puede agregar una regla en tercer lugar, muy específica. Esta ruta enrutan directamente los Estados que destine de cualquier dirección de subred local de hello puede simplemente (NextHopType = VNETLocal).
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
5. Por último, con la tabla de enrutamiento de hello crean y rellenan con un rutas definidas por el usuario, tabla de hello debe ser subred tooa enlazado. En el script de Hola, tabla de rutas de front-end de hello también es dependiente toohello subred de front-end. Este es el script de enlace de hello para la subred de back-end de Hola.
   
     Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
   
        -SubnetName $BESubnet `
        -RouteTableName $BERouteTableName

## <a name="ip-forwarding"></a>reenvío de IP
Un tooUDR de característica complementaria, es el reenvío IP. Se trata de una configuración en un dispositivo Virtual que permita el tráfico de tooreceive no específicamente dirigidos toohello dispositivo y, a continuación, reenviar ese destino final de tooits de tráfico.

Por ejemplo, si el tráfico de AppVM01 hace que un servidor de DNS01 toohello de solicitud, UDR enrutaría este firewall toohello. Con el reenvío IP habilitada, se aceptarán por dispositivo de hello (10.0.0.4) y, a continuación, reenvía el destino último tooits (10.0.2.4) tráfico hello para el destino de hello DNS01 (10.0.2.4). Sin el reenvío IP habilitado en hello Firewall, tráfico no haría aceptado por dispositivo de Hola a pesar de la tabla de rutas Hola dispone firewall Hola salto siguiente Hola. 

> [!IMPORTANT]
> Es crítico tooremember tooenable el reenvío IP junto con usuario definido el enrutamiento.
> 
> 

Para configurar el reenvío IP se usa un solo comando y puede realizarse durante la creación de la máquina virtual. Para hello flujo de este fragmento de código de ejemplo Hola es hacia el final de hello del script de Hola y agrupado con comandos de Hola UDR:

1. Llame a la instancia de la máquina virtual de Hola que es su dispositivo virtual, Hola firewall en este caso y habilitar el reenvío IP (tenga en cuenta; cualquier elemento de rojo que comienza con un signo de dólar (p. ej.: $VMName[0]) es una variable definida por el usuario desde un script de Hola en la sección de referencia de Hola de este documento. Hola cero entre corchetes, [0], representa Hola primera VM de matriz de Hola de máquinas virtuales, para toowork de script de ejemplo de Hola sin modificaciones, debe ser la primera máquina virtual (VM 0) de Hola Hola firewall):
   
     Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | `
   
        Set-AzureIPForwarding -Enable

## <a name="network-security-groups-nsg"></a>Grupos de seguridad de red (NSG)
En este ejemplo, se crea un grupo de seguridad de red y se carga después una única regla. Este grupo es, a continuación, enlazar sólo toohello front-end y back-end subredes (y no Hola SecNet). Mediante declaración se va a compilar Hola siguiente regla:

1. Todo (todos los puertos) el tráfico de hello Internet toohello se deniega todo red virtual (todas las subredes)

Aunque en este ejemplo se usan grupos de seguridad de red, su principal objetivo es constituir un segundo nivel de defensa frente a errores de configuración manual. Queremos tooblock tráfico todo el tráfico entrante de hello tooeither de internet Hola front-end o subredes de back-end, el tráfico solo deben fluya a través de Hola firewall de toohello de subred SecNet (y a continuación si adecuados en toohello front-end o back-end de subredes). Además, con las reglas UDR de hello en su lugar, todo el tráfico que ha llegado en hello subredes front-end o back-end se dirigirá out toohello firewall (gracias tooUDR). firewall de Hola que vea esto como un flujo asimétrico y reduciría el tráfico saliente Hola. Por tanto, hay tres niveles de Hola de protección de seguridad front-end y back-end subredes; (1) no tiene extremos abiertos en hello FrontEnd001 y BackEnd001 servicios en la nube, (2) NSG denegar el tráfico de Internet, firewall de hello (3) quitar tráfico asimétrico de Hola.

Un punto interesante sobre Hola grupo de seguridad de red en este ejemplo es que contiene una única regla, que se muestra a continuación, que es toodeny internet tráfico toohello toda red virtual que incluiría la subred de seguridad de Hola. 

    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet `
        from hello Internet" `
        -Type Inbound -Priority 100 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *

Sin embargo, puesto que hello NSG solo está enlazado toohello front-end y back-end subredes, no procesa Hola regla en el tráfico de subred de seguridad toohello de entrada. Como resultado, incluso si la regla NSG Hola no indica ninguna dirección de tooany del tráfico de Internet en Hola de red virtual, porque hello que NSG nunca fue enlazado toohello subred de seguridad, el tráfico fluirá toohello subred de seguridad.

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $FESubnet -VirtualNetworkName $VNetName

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $BESubnet -VirtualNetworkName $VNetName

## <a name="firewall-rules"></a>Reglas de firewall
En firewall de hello, las reglas de reenvío debe toobe creado. Puesto que firewall de hello es tráfico de bloqueo o reenvío todo el tráfico entrante, saliente y intra-red virtual son necesarias muchas reglas de firewall. Además, todo el tráfico entrante llegará a la dirección IP pública de hello servicio de seguridad (en puertos diferentes), toobe procesados por firewall de Hola. Una práctica recomendada es flujos lógicos de hello toodiagram antes de configurar la repetición de tooavoid de reglas de firewall y subredes de hello más tarde. Hello siguiente ilustración es una vista lógica de reglas de firewall de hello en este ejemplo:

![Vista lógica de hello las reglas de Firewall][2]

> [!NOTE]
> En función de hello que usa el dispositivo de red Virtual, los puertos de administración de hello varían. En este ejemplo se hace referencia a un firewall Barracuda NextGen que utiliza los puertos 22, 801 y 807. Consulte Hola dispositivo proveedor documentación toofind Hola exacta puertos utilizados para la administración de dispositivos Hola usándola.
> 
> 

### <a name="logical-rule-description"></a>Descripción de las reglas de firewall
En el diagrama lógico Hola anterior, subred de seguridad de hello no se muestra ya que firewall de hello es el único recurso al que hello en la subred, y este diagrama muestra las reglas de firewall de Hola y cómo lógicamente permitir o denegación flujos de tráfico y no Hola enrutado ruta de acceso real. Además, puertos externos Hola seleccionados para hello tráfico de RDP son puertos rango superior (8014 – 8026) y se han seleccionado toosomewhat alinear con hello última dos octetos de la dirección IP local de Hola para mejorar la legibilidad sea más fácil (por ejemplo, dirección de servidor local 10.0.1.4 está asociado puerto externo 8014), sin embargo podría utilizarse ninguno de los puertos no conflictivos superior.

En este ejemplo, necesitamos siete tipos de reglas que se describen a continuación:

* Reglas externas (para el tráfico entrante):
  1. Regla de Firewall de administración: Esta regla de redirección de la aplicación permite que los puertos de administración de tráfico toopass toohello del dispositivo de hello red virtual.
  2. Las reglas de RDP (para cada servidor de windows): estos cuatro reglas (uno para cada servidor) le permitirá la administración de hello servidores individuales a través de RDP. Esto se podría incluirse también en una regla de función de las capacidades de Hola de hello de dispositivo de red Virtual que se va a usar.
  3. Las reglas de tráfico de aplicación: Hay dos reglas de tráfico de la aplicación, Hola primero para el tráfico de web front-end de Hola y Hola en segundo lugar para el tráfico de back-end de hello (por ejemplo, la capa del toodata servidor web). configuración de Hola de estas reglas dependerá de arquitectura de red de hello (donde se colocan los servidores) y flujos de tráfico (el tráfico de Hola de qué dirección fluye y qué puertos se usan).
     * primera regla de Hola permitirá a servidor de aplicaciones de hello aplicación real tráfico tooreach Hola. Mientras hello otras reglas permiten para la seguridad, administración, etc., reglas de aplicación son los que permiten tooaccess de los usuarios o servicios externos Hola aplicaciones. En este ejemplo, hay un único servidor web en el puerto 80, lo que una única aplicación regla de firewall redirigirá el tráfico entrante toohello externo IP, dirección IP interna de servidores de web de toohello. Hola redirigido sesión tráfico podría ser NAT tenía toohello interno del servidor.
     * Hola es la segunda regla de tráfico de la aplicación Hola back-end regla tooallow hello Web tootalk toohello AppVM01 servidor (pero no AppVM02) a través de cualquier puerto.
* Reglas internas (para el tráfico entre redes virtuales)
  1. Regla de salida tooInternet: esta regla para permitir el tráfico de cualquier red toopass toohello seleccionado redes. Esta regla suele ser una regla predeterminada ya en firewall de hello, pero en un estado deshabilitado. Esta regla debe habilitarse para este ejemplo.
  2. Regla DNS: Esta regla permite a sólo DNS (el puerto 53) tráfico toopass toohello servidor DNS. Para este entorno que se bloquea la mayor parte del tráfico de hello front-end toohello back-end, esta regla se lo permita específicamente DNS desde cualquier subred local.
  3. Subred tooSubnet regla: esta regla es tooallow cualquier servidor de copia de hello Terminar server de tooany de subred tooconnect de subred de front-end de hello (pero no Hola inversa).
* Regla para notificaciones de error (para el tráfico que no cumple alguna de hello anterior):
  1. Denegar todas las reglas de tráfico: Esto siempre debe ser regla final de hello (en términos de prioridad) y por lo tanto si el tráfico de un flujo se produce un error toomatch cualquiera de hello anteriores se eliminarán por esta regla de reglas. Esta es una regla predeterminada y normalmente está activada; normalmente no se necesitan modificaciones.

> [!TIP]
> En la regla de tráfico de aplicación segundo hello, cualquier puerto está permitido para fácil de este ejemplo, Hola de un escenario real más específicos puertos e intervalos de direcciones deben ser la superficie expuesta a ataques hello tooreduce usadas de esta regla.
> 
> 

<br />

> [!IMPORTANT]
> Una vez que se crean todos Hola por encima de las reglas, es importante tooreview prioridad Hola el tráfico de tooensure de cada regla se permitirá o denegará según sea necesario. En este ejemplo, reglas de hello están en orden de prioridad. Es fácil toobe bloqueado fuera del firewall de hello debido ordenados toomis reglas. Como mínimo, asegúrese de administración de Hola para firewall de hello propio siempre es regla de prioridad más alta absoluta Hola.
> 
> 

### <a name="rule-prerequisites"></a>Requisitos previos de las reglas
Un requisito previo de firewall Hola Máquina Virtual de ejecución Hola son extremos públicos. Para el tráfico de hello firewall tooprocess extremos públicos de hello adecuada deben estar abiertos. Hay tres tipos de tráfico en este ejemplo; (1) administración tráfico toocontrol Hola firewall y las reglas de firewall, servidores de windows RDP (2) el tráfico toocontrol hello y tráfico de la aplicación (3). Estos son tres columnas de tipos de tráfico de hello superior de Hola la mitad de la vista lógica de reglas de firewall de hello anteriores.

> [!IMPORTANT]
> Un takeway clave aquí es tooremember que **todos los** tráfico procederá a través de firewall de Hola. Toohello de escritorio tooremote por lo que el servidor IIS01, aunque se encuentre en el servicio de nube de Front-End de Hola y de subred de Front-End de hello, tooaccess este servidor se va a necesitar tooRDP toohello firewall en 8014 de puerto y, a continuación, Permitir solicitud RDP de hello firewall tooroute Hola internamente toohello IIS01 el puerto de RDP. Hola "Conectar" del portal de Azure botón no funcionará porque no hay ningún tooIIS01 de ruta de acceso directo de RDP (lo que puede ver el portal de hello). Esto significa que todas las conexiones desde Hola internet estarán toohello servicio de seguridad y un puerto, p. ej. secscv001.cloudapp.net:xxxx (Hola de referencia por encima del diagrama para la asignación de hello del puerto externo y dirección IP interna y el puerto).
> 
> 

Un punto de conexión puede abrirse en tiempo de Hola de creación de máquinas virtuales o publicar compilación tal y como se hace en el script de ejemplo de Hola y se muestra a continuación en este fragmento de código (tenga en cuenta; cualquier elemento que comienza con un signo de dólar (p. ej.: $VMName[$i]) es una variable definida por el usuario desde un script de Hola en referencia de Hola sección de CE de este documento. Hola "$i" entre corchetes, [$i] representa número de la matriz de Hola de una VM específica en una matriz de máquinas virtuales):

    Add-AzureEndpoint -Name "HTTP" -Protocol tcp -PublicPort 80 -LocalPort 80 `
        -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | `
        Update-AzureVM

Aunque no claramente que se muestra aquí debido toohello uso de las variables, pero los puntos de conexión son **sólo** abiertos en hello seguridad de servicio en la nube. Se trata de tooensure que se controla todo el tráfico entrante (enrutan, NAT tenía, quitarla) por firewall de Hola.

Un cliente de administración deberá toobe instalado en un servidor de seguridad de PC toomanage hello y crear configuraciones de hello necesarias. Vea proveedor de documentación de su firewall (o en otro NVA) hello en cómo toomanage Hola dispositivo. resto de Hola de esta sección y la siguiente sección hello, creación de reglas de Firewall, describirá configuración Hola de firewall de hello, a través del cliente de administración de proveedores de hello (es decir, no Hola portal de Azure o PowerShell).

Instrucciones para la descarga de cliente y conexión toohello Barracuda utilizado en este ejemplo pueden encontrarse aquí: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)

Una vez iniciada sesión en firewall de hello pero antes de crear las reglas de firewall, hay dos clases de requisitos previos de objeto que pueden facilitar la creación de reglas de hello; Objetos de servicio y de red.

En este ejemplo, tres objetos de red con nombre deben ser definida (uno para la subred de front-end de Hola y subred de back-end de hello, también un objeto de red para la dirección IP de hello del servidor DNS de hello). toocreate una red con nombre; a partir de panel de cliente de administración de dispositivo Barracuda NG hello, vaya la ficha de configuración de toohello, en la sección de configuración operativa hello, haga clic en el conjunto de reglas, a continuación, haga clic en "Redes" en el menú de objetos de servidor de seguridad de Hola y haga clic en nuevo en el menú Editar redes de Hola. objeto de red de Hello ahora se puede crear, mediante la adición de nombre de Hola y un prefijo de hello:

![Creación de un objeto de red front-end][3]

Esto creará una red con nombre para la subred de front-end de hello, se debe crear un objeto similar para así la subred de back-end de Hola. Ahora subredes Hola pueden indicarse más fácilmente por nombre en las reglas de firewall de Hola.

Para hello objeto de servidor DNS:

![Creación de un objeto de servidor DNS][4]

Esta referencia de dirección IP solo se utilizará en una regla DNS más adelante en el documento de Hola.

objetos de requisitos previos segundo Hola son objetos de servicios. Estos representan puertos de conexión RDP de Hola para cada servidor. Puesto que el objeto de servicio RDP existente de hello es el puerto RDP de toohello enlazados de forma predeterminada, 3389, nuevos servicios pueden crearse tooallow tráfico de puertos externos de hello (8014-8026). Hola nuevo puertos también podrían agregarse toohello servicio RDP existente, pero para facilitar la demostración, se puede crear una regla individual para cada servidor. toocreate una nueva regla RDP para un servidor; desde el panel de cliente de administración de dispositivo Barracuda NG hello, navegue toohello ficha de configuración, en hello configuración operativa sección haga clic en el conjunto de reglas, a continuación, haga clic en "Servicios" en hello menú de objetos de servidor de seguridad, desplácese hacia abajo de la lista de hello de servicios y seleccione Hola Servicio "RDP". Haga con el botón derecho y seleccione Copiar; después, haga clic con el botón derecho y seleccione Pegar. Ahora hay un objeto de servicio RDP-Copy1 que se puede editar. Haga clic en Copy1 RDP y seleccione Editar, Hola Editar objeto de servicio ventana se abrirá como se muestra aquí:

![Copia de la regla predeterminada de RDP][5]

valores de Hello, a continuación, pueden ser editado toorepresent Hola servicio RDP para un servidor específico. Para hello AppVM01 anteriormente predeterminado regla RDP debe ser modificada tooreflect un nuevo nombre de servicio, descripción, y utiliza el puerto de RDP externo en hello diagrama de la figura 8 (Nota: se cambian los puertos de Hola de hello predeterminada RDP 3389 toohello del puerto de externo que se va a utilizar para este servidor específico, en caso de hello de puerto externo de hello AppVM01 es 8025) hello servicio modificado se se muestra a continuación:

![Regla de AppVM01][6]

Este proceso debe ser repetida toocreate servicios de RDP para hello restantes servidores; AppVM02, DNS01 y IIS01. creación de Hello de estos servicios realizará creación de reglas de hello más sencillo y más obvio en la sección siguiente Hola.

> [!NOTE]
> Un servicio RDP para hello Firewall no es necesario por dos razones; firewall de hello (1) la primera máquina virtual es una imagen de basadas en Linux, por lo que se usarían SSH en el puerto 22 para la administración de máquinas virtuales en lugar de RDP y (2) el puerto 22 y otros dos puertos de administración se permiten en hello primera regla de administración se describe a continuación tooallow para la conectividad de administración.
> 
> 

### <a name="firewall-rules-creation"></a>Creación de reglas de firewall
En este ejemplo se usan tres tipos de reglas de firewall, todas ellas con iconos distintos:

una regla de redireccionamiento de la aplicación Hello: ![icono de redirigir la aplicación][7]

regla de NAT de destino de Hello: ![icono de NAT de destino][8]

regla de paso de Hello: ![pasar icono][9]

Obtener más información sobre estas reglas puede encontrarse en el sitio web de hello Barracuda.

toocreate Hola siguiendo reglas (o comprobar las reglas existentes de forma predeterminada), a partir de panel de cliente de administración de dispositivo Barracuda NG hello, vaya la ficha de configuración de toohello, Hola configuración operativa sección, haga clic en el conjunto de reglas. Llama a una cuadrícula, "Main reglas" mostrará Hola existente las reglas activas y desactivadas en este servidor de seguridad. En hello superior derecha de esta cuadrícula es una pequeña, de color verde "+" botón, haga clic en este toocreate una nueva regla (Nota: el firewall puede "bloquear" para los cambios, si ve un botón de marca "Bloqueo" y son no se puede toocreate o editar reglas, haga clic en este botón demasiado "desbloquear" Hola SAR de regla t y permitir la edición). Si desea tooedit una regla existente, seleccione esa regla, haga clic en y seleccione Editar regla.

Una vez que las reglas se crea o modifica, se deben insertar toohello firewall y, a continuación, activar, si no es así regla Hola cambios no surtirán efecto. proceso de activación e inserción de Hola se describe a continuación las descripciones de reglas de detalles de Hola.

detalles de Hola de cada regla necesario toocomplete en este ejemplo se describe como sigue:

* **Regla de administración de Firewall**: una regla de redireccionamiento de esta aplicación permite el tráfico toopass toohello los puertos de administración del dispositivo Hola red virtual, en este ejemplo un Barracuda NextGen Firewall. puertos de administración de Hello estén 801, 807 y, opcionalmente, 22. puertos internos y externos de Hola se Hola iguales (es decir, ninguna traducción de puerto). SETUP-MGMT-ACCESS es una regla predeterminada y está habilitada de forma predeterminada (en Barracuda NextGen Firewall versión 6.1).
  
    ![Regla de administración de firewall][10]

> [!TIP]
> Hello espacio de direcciones de origen en esta regla es cualquier, si hello se conocen los intervalos de direcciones IP de administración, lo que reduce este ámbito también reduciría puertos de administración de toohello superficie de ataque de Hola.
> 
> 

* **Reglas de RDP**: reglas NAT de destino de estos le permitirá la administración del programa Hola a servidores individuales a través de RDP.
  Hay cuatro toocreate crítico campos necesarios de esta regla:
  
  1. Origen: tooallow RDP desde cualquier lugar, referencia de Hola "Cualquiera" se usa en el campo de origen de Hola.
  2. Servicio: usar hello objeto adecuado de servicio creado anteriormente, en este caso "AppVM01 RDP", puertos externos Hola redirección la dirección IP local del servidor toohello y tooport 3386 (puerto RDP de hello predeterminado). Esta regla concreta es para tooAppVM01 de acceso RDP.
  3. Destino: debe ser hello *puerto local en el servidor de seguridad de hello*, "DCHP 1 IP Local" o eth0 si usa direcciones IP estáticas. número ordinal de Hello (eth0, eth1, etcetera) puede ser diferente si el dispositivo de red tiene varias interfaces locales. Éste es el puerto de hello firewall Hola envía desde (pueden ser Hola igual como Hola puerto de recepción), destino enrutado real Hola se encuentre en el campo de la lista de destinos de Hola.
  4. Redirección: esta sección explica el dispositivo virtual de Hola donde tooultimately redirigir este tráfico. Hola la redirección más sencilla es tooplace Hola IP y puerto (opcional) en el campo de la lista de destinos de Hola. Si ningún puerto es el puerto de destino de hello usado en la solicitud entrante de hello será usa (es decir, ninguna traducción), si no se designa un puerto de puerto de hello también será NAT junto con IP Hola se referiría.
     
     ![Regla de RDP de firewall][11]
     
     Un total de cuatro reglas RDP necesitará toobe creado: 
     
     | Nombre de la regla | Server | Servicio | Lista de destinos |
     | --- | --- | --- | --- |
     | RDP a IIS01 |IIS01 |IIS01 RDP |10.0.1.4:3389 |
     | RDP a DNS01 |DNS01 |DNS01 RDP |10.0.2.4:3389 |
     | RDP a AppVM01 |AppVM01 |AppVM01 RDP |10.0.2.5:3389 |
     | RDP a AppVM02 |AppVM02 |AppVm02 RDP |10.0.2.6:3389 |

> [!TIP]
> Restricción hacia abajo el ámbito de Hola de hello origen y campos de servicio se reducirá la superficie expuesta a ataques Hola. ámbito de Hello más limitada que le permitirá funcionalidad debe utilizarse.
> 
> 

* **Las reglas de tráfico de aplicación**: hay dos reglas de tráfico de aplicaciones, Hola primero para el tráfico de web front-end de Hola y Hola en segundo lugar para el tráfico de back-end de hello (por ejemplo, la capa del toodata servidor web). Estas reglas dependerá de arquitectura de red de hello (donde se colocan los servidores) y flujos de tráfico (el tráfico de Hola de qué dirección fluye y qué puertos se usan).
  
    Se describe en primer lugar es la regla de front-end de hello para el tráfico web:
  
    ![Regla de Web de firewall][12]
  
    Esta regla de NAT de destino permite que servidor de aplicaciones de hello aplicación real tráfico tooreach Hola. Mientras hello otras reglas permiten para la seguridad, administración, etc., reglas de aplicación son los que permiten tooaccess de los usuarios o servicios externos Hola aplicaciones. En este ejemplo, hay un único servidor web en el puerto 80, por lo tanto Hola única aplicación regla de firewall redirigirá el tráfico entrante toohello externo IP, dirección IP interna de servidores de web de toohello.
  
    **Tenga en cuenta**: que no hay ningún puerto asignado en el campo de la lista de destinos de Hola, por lo tanto hello entrante puerto 80 (o 443 para hello servicio seleccionado) se utilizará en la redirección de Hola Hola del servidor de web. Si el servidor web de hello está escuchando en un puerto diferente, por ejemplo, el puerto 8080, campo de la lista de destinos de hello podría ser tooallow too10.0.1.4:8080 actualizada para así la redirección de puertos de Hola.
  
    Hola es la siguiente regla de tráfico de aplicación Hola back-end regla tooallow hello Web tootalk toohello AppVM01 servidor (pero no AppVM02) a través de cualquier servicio:
  
    ![Regla de AppVM01 de firewall][13]
  
    Esta regla de paso permite que cualquier servidor IIS en Hola de tooreach de subred de front-end de hello AppVM01 (dirección IP 10.0.2.5) en cualquier puerto, con los datos de tooaccess de protocolo necesarios para la aplicación web de hello.
  
    En esta captura de pantalla de un "\<explícita dest\>" se usa en toosignify de campo de destino de hello 10.0.2.5 como destino de Hola. Esto podría ser explícita denominada tal como se muestra, o un objeto de red (como ocurría en los requisitos previos de hello para el servidor DNS de hello). Esto es toohello administrador del servidor de seguridad de hello ya se usará el método toowhich. tooadd 10.0.2.5 como un Explict Desitnation, haga doble clic en la primera fila en blanco hello en \<explícita dest\> y escriba la dirección de hello en ventana hello que aparece.
  
    Con esta regla pasa, no se necesita ninguna NAT puesto que se trata el tráfico interno, por lo que Hola método de conexión puede establecerse demasiado "SNAT n".
  
    **Tenga en cuenta**: red de origen de hello en esta regla es cualquier recurso de subred de front-end de hello, si sólo habrá uno, o un número específico de servidores web, un objeto de red pudieron ser recursos creada toobe direcciones toothose IP exactas más específicas en lugar de subred de front-end de Hello completa.

> [!TIP]
> Esta regla usa el servicio de Hola "Cualquiera" toomake toosetup más fácil de aplicación de ejemplo de Hola y usar, esto también le permitirá ICMPv4 (ping) en una sola regla. Sin embargo, este no es el procedimiento recomendado. Hola puertos y protocolos ("servicios") deben ser toohello limitados mínima posible que permite la superficie expuesta a ataques aplicación operación tooreduce Hola a través de este límite.
> 
> 

<br />

> [!TIP]
> Aunque esta regla muestra una referencia explícita dest que se va a utilizar, debe utilizarse un enfoque coherente en toda la configuración del firewall Hola. Se recomienda que Hola denominado objeto de red usarán en todo para facilitar la legibilidad y compatibilidad. Hola explícita-dest es usado tooshow solo aquí un método alternativo de referencia y generalmente no se recomienda (especialmente en configuraciones complejas).
> 
> 

* **Regla de salida tooInternet**: pasar esta regla para permitir el tráfico de las redes de destino de origen red toopass toohello seleccionado. Esta regla es una regla predeterminada ya vienen en firewall de Barracuda NextGen hello, pero está en un estado deshabilitado. Haga doble clic en esta regla puede tener acceso a comandos de activar la regla de Hola. regla de Hola que se muestra aquí ha sido modificado tooadd Hola dos subredes locales que se crearon como referencias en la sección de requisitos previos de Hola de este atributo de origen de toohello de documento de esta regla.
  
    ![Regla de salida de firewall][14]
* **Regla de DNS**: pasar esta regla permite sólo DNS (el puerto 53) tráfico toopass toohello servidor DNS. Para este entorno que se bloquea la mayor parte del tráfico de hello front-end toohello back-end, esta regla permite específicamente DNS.
  
    ![Regla de DNS de firewall][15]
  
    **Tenga en cuenta**: en esta pantalla se incluye Hola instantánea método de conexión. Dado que esta regla es para el tráfico interno de dirección IP de toointernal IP, no se requiere ninguna traducción, este Hola método de conexión se establece demasiado "No SNAT" para esta regla de paso.
* **Subred tooSubnet regla**: pasar esta regla es una regla predeterminada que se ha activado y modificado tooallow cualquier servidor de hello volver Terminar server tooany de subred tooconnect en Hola subred de front-end. Esta regla es el tráfico interno de todos los por lo que se puede establecer tooNo SNAT Hola método de conexión.
  
    ![Regla entre redes virtuales de firewall][16]
  
    **Tenga en cuenta**: Hola bidireccional casilla no está activada (ni está activada en la mayoría de las reglas), esto es significativo para esta regla ya que esto dificulta "uno direccional" de la regla, se puede iniciar una conexión de red de front-end del toohello Hola de subred de back-end, pero no Hola inversa. Si esa casilla se activa, esta regla permitiría el tráfico bidireccional lo que, desde la perspectiva de nuestro diagrama lógico, no es deseable.
* **Denegar todas las reglas de tráfico**: siempre debería ser regla final de hello (en términos de prioridad) y, como por ejemplo, si un tráfico fluye se produce un error toomatch cualquiera de hello anterior reglas se eliminarán por esta regla. Esta es una regla predeterminada y normalmente está activada; normalmente no se necesitan modificaciones. 
  
    ![Regla de denegación de firewall][17]

> [!IMPORTANT]
> Una vez que se crean todos Hola por encima de las reglas, es importante tooreview prioridad Hola el tráfico de tooensure de cada regla se permitirá o denegará según sea necesario. En este ejemplo, reglas de Hola están en orden de hello deben aparecer en hello cuadrícula principal de las reglas en hello Barracuda Management Client de reenvío.
> 
> 

## <a name="rule-activation"></a>Activación de reglas
Hola ruleset que se modificó la especificación de toohello de diagrama de la lógica de hello, debe ser Hola ruleset cargado toohello firewall y, a continuación, se activa.

![Activación de reglas de firewall][18]

En la esquina superior derecha de Hola de cliente de administración de hello son un clúster de botones. Haga clic en firewall de Hola "enviar cambios" botón toosend Hola modificar reglas toohello, a continuación, haga clic en el botón de "Activar" Hola.

Con la activación de Hola de conjunto de reglas de firewall de hello esta compilación de entorno de ejemplo está completa.

## <a name="traffic-scenarios"></a>Escenarios de tráfico
> [!IMPORTANT]
> Una clave takeway es tooremember que **todos los** tráfico procederá a través de firewall de Hola. Toohello de escritorio tooremote por lo que el servidor IIS01, aunque se encuentre en el servicio de nube de Front-End de Hola y de subred de Front-End de hello, tooaccess este servidor se va a necesitar tooRDP toohello firewall en 8014 de puerto y, a continuación, Permitir solicitud RDP de hello firewall tooroute Hola internamente toohello IIS01 el puerto de RDP. Hola "Conectar" del portal de Azure botón no funcionará porque no hay ningún tooIIS01 de ruta de acceso directo de RDP (lo que puede ver el portal de hello). Esto significa que todas las conexiones desde Hola internet estarán toohello servicio de seguridad y un puerto, por ejemplo, secscv001.cloudapp.net:xxxx.
> 
> 

Para estos escenarios, debe ser Hola siguiendo las reglas de firewall en su lugar:

1. Administración del firewall
2. TooIIS01 RDP
3. TooDNS01 RDP
4. TooAppVM01 RDP
5. TooAppVM02 RDP
6. Toohello de tráfico de la aplicación Web
7. Tráfico de aplicación tooAppVM01
8. Salida toohello Internet
9. TooDNS01 de front-end
10. Tráfico de subredes intra (back-end toofront final solamente)
11. Denegar todo

conjunto de reglas de firewall real Hola probablemente tendrá muchas otras reglas en toothese adición, reglas de Hola en cualquier servidor de seguridad determinado también tendrá números de prioridad diferentes de los que se enumeran aquí Hola a. Esta lista y números asociados son tooprovide relevancia entre simplemente estas once reglas y la prioridad relativa de hello entre ellos. En otras palabras; en firewall de hello real, Hola "RDP tooIIS01" puede ser el número de regla 5, pero mientras está por debajo de la regla de "Administración de Firewall" hello y versiones posteriores de la regla de "RDP tooDNS01" hello podrían alinearse con intención de Hola de esta lista. También le ayudará a lista de Hola Hola escenarios permitiendo brevedad; p. ej. “Regla de reenvío 9 (DNS)”. Para mayor brevedad, Hola cuatro reglas RDP será colectivamente el acrónimo, "Hola reglas RDP" al escenario de tráfico de hello es tooRDP no relacionado.

Recuerde también que los grupos de seguridad de red están vigentes para el tráfico entrante de internet en hello front-end y back-end subredes.

#### <a name="allowed-internet-tooweb-server"></a>(Permitido) Internet tooWeb Server
1. El usuario de Internet solicita la página HTTP desde SecSvc001.CloudApp.Net (servicio en la nube accesible desde Internet).
2. Fases de tráfico del servicio de nube a través de un extremo abierto en la interfaz de toofirewall del puerto 80 en 10.0.0.4:80
3. No hay NSG asignada subred tooSecurity, de modo que las reglas NSG de sistema permitir el tráfico toofirewall
4. Tráfico llega a dirección IP interna del servidor de seguridad de hello (10.0.1.4)
5. El firewall comienza el procesamiento de las reglas:
   1. No se aplican, mover toonext regla FW regla 1 (FW Mgmt)
   2. Reglas de Firewall 2 y 5 (reglas de RDP) no se aplican, mover toonext regla
   3. FW regla 6 (aplicación: Web) aplican, se permite el tráfico, firewall NAT too10.0.1.4 (IIS01)
6. subred de front-end de Hello comienza el procesamiento de la regla de entrada:
   1. NSG de la regla 1 (bloque de Internet) no se aplica (este tráfico fue NAT estuviera firewall hello, por tanto, la dirección de origen de hello ahora es firewall de Hola que se encuentra en la subred de seguridad de Hola y visto por subred de front-end de hello tráfico NSG toobe "local" y, por tanto, se permite), mover toonext regla
   2. Reglas de NSG predeterminada permitir el tráfico de toosubnet de subred, se permite el tráfico, detenga el procesamiento de la regla NSG
7. Iis01 escucha el tráfico de web, recibe esta solicitud y comienza a procesar la solicitud de Hola
8. Iis01 intenta tooinitiates un tooAppVM01 de sesión FTP en la subred de back-end
9. ruta UDR Hola de subred de front-end hace Hola firewall Hola de próximo salto
10. No hay reglas de salida en la subred front-end, se permite el tráfico.
11. El firewall comienza el procesamiento de las reglas:
    1. No se aplican, mover toonext regla FW regla 1 (FW Mgmt)
    2. No se aplican reglas FW 2 y 5 (reglas de RDP), mover toonext regla
    3. FW regla 6 (aplicación: Web) no se aplican, mover toonext regla
    4. 7 de la regla de FW (aplicación: back-end) se aplican, se permite el tráfico, firewall reenvía el tráfico too10.0.2.5 (AppVM01)
12. subred de back-end de Hello comienza el procesamiento de la regla de entrada:
    1. Regla de NSG 1 (bloque de Internet) no se aplica, mover toonext regla
    2. Reglas de NSG predeterminada permitir el tráfico de toosubnet de subred, se permite el tráfico, detenga el procesamiento de la regla NSG
13. AppVM01 recibe la solicitud de Hola e inicia la sesión de Hola y responde
14. ruta UDR Hola de subred de back-end hace Hola firewall Hola de próximo salto
15. Puesto que no hay ninguna regla NSG saliente en hello respuesta de Hola de subred de back-end se permite
16. Dado que esto está devolviendo el tráfico en una sesión establecida Hola del firewall pasa servidor web de toohello de espera de respuesta hello (IIS01)
17. La subred front-end comienza el procesamiento de las reglas de entrada:
    1. Regla de NSG 1 (bloque de Internet) no se aplica, mover toonext regla
    2. Reglas de NSG predeterminada permitir el tráfico de toosubnet de subred, se permite el tráfico, detenga el procesamiento de la regla NSG
18. servidor IIS de Hola recibe respuesta Hola, completa la transacción de hello con AppVM01 y, a continuación, complete creación Hola respuesta HTTP, esta respuesta HTTP se envía toohello solicitante
19. Puesto que no hay ninguna regla NSG saliente en hello respuesta de Hola de subred de front-end está permitido
20. Hola firewall de Hola de aciertos de respuesta HTTP y porque se trata de hello respuesta tooan establecido sesión NAT se acepta por firewall de Hola
21. firewall de Hello, a continuación, redirige Hola respuesta atrás toohello usuario de Internet
22. Puesto que no existen reglas de NSG salida ni saltos UDR de subred de front-end de Hola se permita la respuesta de Hola y Hola usuario de Internet recibe hello web página solicitada.

#### <a name="allowed-internet-rdp-toobackend"></a>(Permitido) TooBackend de RDP de Internet
1. Administrador del servidor en internet solicita tooAppVM01 de sesión RDP mediante SecSvc001.CloudApp.Net:8025, donde 8025 es número de puerto asignados al usuario de Hola de regla de firewall "RDP tooAppVM01" hello
2. servicio de nube de Hello pasa el tráfico a través del extremo abierto de hello en interfaz del puerto 8025 toofirewall 10.0.0.4:8025
3. No hay NSG asignada subred tooSecurity, de modo que las reglas NSG de sistema permitir el tráfico toofirewall
4. El firewall comienza el procesamiento de las reglas:
   1. No se aplican, mover toonext regla FW regla 1 (FW Mgmt)
   2. No se aplica la regla FW 2 (RDP IIS), mover toonext regla
   3. No se aplica la regla FW 3 (RDP DNS01), mover toonext regla
   4. Aplicar regla fw4 (RDP AppVM01), se permite el tráfico, firewall NAT se too10.0.2.5:3386 (puerto de RDP en AppVM01)
5. subred de back-end de Hello comienza el procesamiento de la regla de entrada:
   1. NSG de la regla 1 (bloque de Internet) no se aplica (este tráfico fue NAT estuviera firewall hello, por tanto, la dirección de origen de hello ahora es firewall de Hola que se encuentra en la subred de seguridad de Hola y visto por subred de back-end de hello tráfico NSG toobe "local" y, por tanto, se permite), mover toonext regla
   2. Reglas de NSG predeterminada permitir el tráfico de toosubnet de subred, se permite el tráfico, detenga el procesamiento de la regla NSG
6. AppVM01 escucha el tráfico RDP y responde.
7. No hay reglas de grupo de seguridad de red de salida, se aplican las reglas predeterminadas y se permite el tráfico de retorno.
8. UDR enruta el tráfico saliente toohello firewall salto siguiente Hola
9. Porque esto está devolviendo el tráfico en una sesión establecida Hola del firewall pasa usuario de internet de hello respuesta toohello atrás
10. La sesión RDP está habilitada.
11. AppVM01 solicita la contraseña del nombre de usuario.

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a>(Permitido) Búsqueda de DNS del servidor web en el servidor DNS
1. Web necesidades de servidor, IIS01, fuente de distribución de datos en www.data.gov, pero necesita tooresolve Hola dirección.
2. Hola configuración de red para las listas de red virtual de hello DNS01 (10.0.2.4 de subred de back-end de hello) como servidor DNS principal de hello, IIS01 envía Hola DNS solicitud tooDNS01
3. UDR enruta el tráfico saliente toohello firewall salto siguiente Hola
4. Ninguna regla NSG saliente está enlazado toohello subred de front-end, se permite el tráfico
5. El firewall comienza el procesamiento de las reglas:
   1. No se aplican, mover toonext regla FW regla 1 (FW Mgmt)
   2. No se aplican reglas FW 2 y 5 (reglas de RDP), mover toonext regla
   3. No se aplicará la FW reglas 6 y 7 (reglas de aplicaciones), mover toonext regla
   4. No se aplican, mover toonext regla FW regla 8 (tooInternet)
   5. Aplicar FW regla 9 (DNS), se permite el tráfico, firewall reenvía el tráfico too10.0.2.4 (DNS01)
6. subred de back-end de Hello comienza el procesamiento de la regla de entrada:
   1. Regla de NSG 1 (bloque de Internet) no se aplica, mover toonext regla
   2. Reglas de NSG predeterminada permitir el tráfico de toosubnet de subred, se permite el tráfico, detenga el procesamiento de la regla NSG
7. Servidor DNS recibe la solicitud de Hola
8. Servidor DNS no tiene dirección de hello en caché y pide un servidor DNS raíz en hello internet
9. UDR enruta el tráfico saliente toohello firewall salto siguiente Hola
10. No hay reglas de grupo de seguridad de red de salida en la subred back-end, se permite el tráfico.
11. El firewall comienza el procesamiento de las reglas:
    1. No se aplican, mover toonext regla FW regla 1 (FW Mgmt)
    2. No se aplican reglas FW 2 y 5 (reglas de RDP), mover toonext regla
    3. No se aplicará la FW reglas 6 y 7 (reglas de aplicaciones), mover toonext regla
    4. Aplicar reglas de FW 8 (tooInternet), se permite el tráfico, sesión es SNAT out tooroot servidor DNS en Internet de Hola
12. Responde el servidor DNS de Internet, ya que esta sesión se inició en firewall de hello, respuesta de hello acepta firewall Hola
13. Tal y como se trata de una sesión establecida, firewall de hello reenvía Hola respuesta toohello iniciar el servidor, DNS01
14. subred de back-end de Hello comienza el procesamiento de la regla de entrada:
    1. Regla de NSG 1 (bloque de Internet) no se aplica, mover toonext regla
    2. Reglas de NSG predeterminada permitir el tráfico de toosubnet de subred, se permite el tráfico, detenga el procesamiento de la regla NSG
15. servidor DNS de Hello recibe y almacena en caché la respuesta de hello y, a continuación, responde tooIIS01 de espera de solicitud inicial toohello
16. ruta UDR Hola de subred de back-end hace Hola firewall Hola de próximo salto
17. No existe ninguna regla NSG saliente en la subred de back-end de hello, se permite el tráfico
18. Se trata de una sesión establecida en firewall de hello, respuesta de Hola se reenvía por servidor IIS de hello firewall back-toohello
19. La subred front-end comienza el procesamiento de las reglas de entrada:
    1. No hay ninguna regla NSG que se aplica tooInbound tráfico de subred de front-end del toohello Hola de subred de back-end, por lo que no se aplica ninguno de reglas NSG Hola
    2. Hola regla predeterminada del sistema permitiendo el tráfico entre subredes permitiría este tráfico por lo que se permite el tráfico de Hola
20. Iis01 recibe respuesta hello DNS01

#### <a name="allowed-backend-server-toofrontend-server"></a>(Permitido) Servidor de tooFrontend de servidor back-end
1. Un administrador ha iniciado sesión tooAppVM02 a través de RDP solicita un archivo directamente desde el servidor de IIS01 Hola a través del explorador de archivos de windows
2. ruta UDR Hola de subred de back-end hace Hola firewall Hola de próximo salto
3. Puesto que no hay ninguna regla NSG saliente en hello respuesta de Hola de subred de back-end se permite
4. El firewall comienza el procesamiento de las reglas:
   1. No se aplican, mover toonext regla FW regla 1 (FW Mgmt)
   2. No se aplican reglas FW 2 y 5 (reglas de RDP), mover toonext regla
   3. No se aplicará la FW reglas 6 y 7 (reglas de aplicaciones), mover toonext regla
   4. No se aplican, mover toonext regla FW regla 8 (tooInternet)
   5. No se aplica FW regla 9 (DNS), mover toonext regla
   6. Aplicar FW regla 10 (Intra-subred), se permite el tráfico, firewall pasa el tráfico too10.0.1.4 (IIS01)
5. La subred front-end comienza el procesamiento de las reglas de entrada:
   1. Regla de NSG 1 (bloque de Internet) no se aplica, mover toonext regla
   2. Reglas de NSG predeterminada permitir el tráfico de toosubnet de subred, se permite el tráfico, detenga el procesamiento de la regla NSG
6. Suponiendo que autorización y la autenticación correcta, IIS01 acepta la solicitud de Hola y responde
7. ruta UDR Hola de subred de front-end hace Hola firewall Hola de próximo salto
8. Puesto que no hay ninguna regla NSG saliente en hello respuesta de Hola de subred de front-end está permitido
9. Tal y como se trata de una sesión existente en firewall de Hola se permita esta respuesta y firewall de hello devuelve Hola respuesta tooAppVM02
10. La subred back-end comienza el procesamiento de las reglas de entrada:
    1. Regla de NSG 1 (bloque de Internet) no se aplica, mover toonext regla
    2. Reglas de NSG predeterminada permitir el tráfico de toosubnet de subred, se permite el tráfico, detenga el procesamiento de la regla NSG
11. AppVM02 recibe respuesta Hola

#### <a name="denied-internet-direct-tooweb-server"></a>(Denegado) TooWeb directo de Internet Server
1. Usuario de Internet intenta tooaccess Hola servidor web, IIS01, a través de hello FrontEnd001.CloudApp.Net servicio
2. Puesto que no hay ningún extremo abierto para el tráfico HTTP, esto no pasará a través de hello servicio en la nube y no llegar a servidor hello
3. Si los puntos de conexión de hello estaban abiertos por algún motivo, hello NSG (bloque de Internet) en la subred de front-end de hello bloquearían este tráfico
4. Por último, ruta de UDR de subred de front-end de hello enviaría todo el tráfico saliente desde IIS01 toohello firewall como próximo salto de hello, firewall de hello sería y aparecen como tráfico asimétrico Quitar respuesta de salida de hello por lo tanto hay al menos tres capas independientes de defensa entre hello IIS01 e internet a través de su servicio de nube impedir el acceso no autorizado o inadecuado.

#### <a name="denied-internet-toobackend-server"></a>(Denegado) Internet tooBackend Server
1. Usuario de Internet intenta tooaccess un archivo en AppVM01 a través de hello BackEnd001.CloudApp.Net servicio
2. Dado que no hay ningún extremo abierto para el recurso compartido de archivos, esto no sucedería Hola servicio en la nube y no llegar a servidor hello
3. Si los puntos de conexión de hello estaban abiertos por algún motivo, hello NSG (bloque de Internet) bloquearían este tráfico
4. Por último, ruta de hello UDR enviaría todo el tráfico saliente desde AppVM01 toohello firewall como próximo salto de hello, firewall de hello sería y aparecen como tráfico asimétrico Quitar respuesta de salida de hello por lo tanto hay al menos tres capas independientes de defensa entre Hola AppVM01 e internet a través de su servicio de nube impedir el acceso no autorizado o inadecuado.

#### <a name="denied-frontend-server-toobackend-server"></a>(Denegado) Front-end server tooBackend Server
1. Se supone IIS01 se pone en peligro y se ejecuta el código malintencionado intente servidores de subred de back-end de tooscan Hola.
2. ruta de UDR de subred de front-end de Hello enviaría todo el tráfico saliente desde IIS01 toohello firewall salto siguiente Hola. Esto no es algo que puede ser modificado por hello en peligro la máquina virtual.
3. firewall de Hello procesaría tráfico hello, si se ha de solicitud de hello tooAppVM01 o servidor DNS de toohello para las búsquedas DNS que potencialmente se permite el tráfico por firewall de hello (vence tooFW reglas 7 y 9). La regla de reenvío 11 bloquearía todo el tráfico restante (denegar todo).
4. Si la detección de amenazas avanzada se habilitó en firewall de hello (que no se trata en este documento, consulte Hola documentación del fabricante de su dispositivo de red específicas amenaza capacidades avanzadas), incluso el tráfico que se permitan hello básico de reglas de reenvío se describe en este documento puede evitarse si el tráfico de hello contenía firmas conocidas o patrones que se marca una regla avanzada amenaza.

#### <a name="denied-internet-dns-lookup-on-dns-server"></a>(Denegado) Búsqueda de DNS de Internet en el servidor DNS
1. Usuario de Internet intenta toolookup un registro DNS interno en DNS01 a través del servicio BackEnd001.CloudApp.Net 
2. Dado que no hay ningún extremo abierto para el tráfico DNS, esto no pasará a través de hello servicio en la nube y no llegar a servidor hello
3. Si los puntos de conexión de hello estaban abiertos por algún motivo, la regla de NSG de hello (bloque de Internet) en la subred de front-end de hello bloquearían este tráfico
4. Por último, ruta UDR de subred de back-end de hello enviaría todo el tráfico saliente desde DNS01 toohello firewall como próximo salto de hello, firewall de hello sería y aparecen como tráfico asimétrico Quitar respuesta de salida de hello por lo tanto hay al menos tres capas independientes de defensa entre hello DNS01 e internet a través de su servicio de nube impedir el acceso no autorizado o inadecuado.

#### <a name="denied-internet-toosql-access-through-firewall"></a>(Denegado) Acceso a tooSQL de Internet a través del Firewall
1. El usuario de Internet solicita datos SQL desde SecSvc001.CloudApp.Net (servicio en la nube accesible desde Internet).
2. Dado que no hay ningún extremo abierto para SQL, esto no sucedería Hola servicio en la nube y no llegar a firewall de Hola
3. Si los puntos de conexión SQL estaban abiertos por algún motivo, firewall de hello comenzaría procesamiento de reglas:
   1. No se aplican, mover toonext regla FW regla 1 (FW Mgmt)
   2. Reglas de Firewall 2 y 5 (reglas de RDP) no se aplican, mover toonext regla
   3. No se aplicará la FW regla 6 y 7 (reglas de aplicación), mover toonext regla
   4. No se aplican, mover toonext regla FW regla 8 (tooInternet)
   5. No se aplica FW regla 9 (DNS), mover toonext regla
   6. No se aplican, mover toonext regla FW regla 10 (Intra-subred)
   7. Se aplica la regla de reenvío 11 (denegar todo), se permite el tráfico, detener el procesamiento de las reglas.

## <a name="references"></a>Referencias
### <a name="main-script-and-network-config"></a>Script principal y configuración de red
Guardar Hola Script completo en un archivo de script de PowerShell. Guardar configuración de red de hello en un archivo denominado "NetworkConf2.xml".
Modifique las variables definidas por el usuario de hello según sea necesario. Ejecutar script de Hola, a continuación, siga anterior de instrucciones de instalación del regla de Firewall Hola.

#### <a name="full-script"></a>Script completo
Este script superará en función de las variables definidas por el usuario de hello:

1. Conectar tooan suscripción de Azure
2. Creación de una cuenta de almacenamiento nueva
3. Crear una red virtual nueva y tres subredes tal como se define en el archivo de configuración de red de Hola
4. Creación de cinco máquinas virtuales, un firewall y cuatro máquinas virtuales de servidor Windows
5. La configuración del enrutamiento definido por el usuario incluye:
   1. Crear dos nuevas tablas de enrutamiento
   2. Agregar tablas de rutas toohello
   3. Enlazar subredes tooappropriate de tablas
6. Habilitar el reenvío IP en hello NVA
7. Configuración del grupo de seguridad de red, incluido lo siguiente:
   1. Creación de un grupo de seguridad de red
   2. Adición de una regla
   3. Enlace hello NSG toohello las subredes correspondientes

Este script de PowerShell debe ejecutarse localmente en un equipo o servidor conectado a Internet.

> [!IMPORTANT]
> Cuando se ejecuta este script, puede haber advertencias u otros mensajes informativos que se muestran en PowerShell. Solo los mensajes de error indicados en rojo son motivo de preocupación.
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and User Defined Routing in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Three new cloud services
       - Three Subnets (SecNet, FrontEnd, and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet
       - Three Servers on hello BackEnd Subnet
       - IP Forwading from hello FireWall out toohello internet
       - User Defined Routing FrontEnd and BackEnd Subnets toohello NVA

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Everyone's security requirements are different and can be addressed in a myriad of ways.
      Please be sure that any sensitive data or applications are behind hello appropriate
      layer(s) of protection. This script serves as an example of some of hello techniques
      that can be used, but should not be used for all scenarios. You are responsible to
      assess your security needs and hello appropriate protections needed, and then effectively
      implement those protections.

      Security Service (SecNet subnet 10.0.0.0/24)
       myFirewall - 10.0.0.4

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       IIS01      - 10.0.1.4

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
        $SecureService = "SecSvc001"
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $VNetPrefix = "10.0.0.0/16"
        $SecNet = "SecNet"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf3.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # UDR Details
        $FERouteTableName = "FrontEndSubnetRouteTable"
        $BERouteTableName = "BackEndSubnetRouteTable"

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure UDR and IP forwarding is setup
        # properly this script requires VM 0 be hello NVA.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $SecureService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $SecNet
          $VMIP += "10.0.0.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

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

    If (Test-AzureName -Service -Name $SecureService) { 
        Write-Host "hello SecureService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use" -ForegroundColor Green}

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
        New-AzureService -Location $DeploymentLocation -ServiceName $SecureService -ErrorAction Stop
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
                # Note: All traffic goes through hello firewall, so we'll need tooset up all ports here.
                #       Also, hello firewall will be redirecting traffic tooa new IP and Port in a forwarding
                #       rule, so all of these endpoint have hello same public and local port and hello firewall
                #       will do hello mapping, NATing, and/or redirection as declared in hello firewall rules.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPWeb"    -Protocol tcp -PublicPort 8014 -LocalPort 8014 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp1"   -Protocol tcp -PublicPort 8025 -LocalPort 8025 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp2"   -Protocol tcp -PublicPort 8026 -LocalPort 8026 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPDNS01"  -Protocol tcp -PublicPort 8024 -LocalPort 8024 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "RemoteDesktop" | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                }
            $i++
        }

    # Configure UDR and IP Forwarding
        Write-Host "Configuring UDR" -ForegroundColor Cyan

      # Create hello Route Tables
        Write-Host "Creating hello Route Tables" -ForegroundColor Cyan 
        New-AzureRouteTable -Name $BERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $BESubnet subnet"
        New-AzureRouteTable -Name $FERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $FESubnet subnet"

      # Add Routes tooRoute Tables
        Write-Host "Adding Routes toohello Route Tables" -ForegroundColor Cyan 
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $FEPrefix `
            -NextHopType VNETLocal

      # Assoicate hello Route Tables with hello Subnets
        Write-Host "Binding Route Tables toohello Subnets" -ForegroundColor Cyan 
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $BESubnet `
            -RouteTableName $BERouteTableName
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $FESubnet `
            -RouteTableName $FERouteTableName

     # Enable IP Forwarding on hello Virtual Appliance
        Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] `
            |Set-AzureIPForwarding -Enable

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rule
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 100 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

      # Assign hello NSG tootwo Subnets
        # hello NSG is *not* bound toohello Security Subnet. hello result
        # is that internet traffic flows only toohello Security subnet
        # since hello NSG bound toohello Frontend and Backback subnets
        # will Deny internet traffic toothose subnets.
        Write-Host "Binding hello NSG tootwo subnets" -ForegroundColor Cyan
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
              <Subnet name="SecNet">
                <AddressPrefix>10.0.0.0/24</AddressPrefix>
              </Subnet>
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
[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "Red perimetral bidireccional con un dispositivo de red virtual, grupos de seguridad de red y enrutamiento definido por el usuario"
[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Vista lógica de hello las reglas de Firewall"
[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "Creación de un objeto de red front-end"
[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "Creación de un objeto de servidor DNS"
[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "Copia de la regla predeterminada de RDP"
[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "Regla de AppVM01"
[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "Icono de redirección de aplicación"
[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "Icono de NAT de destino"
[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "Icono de Paso"
[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "Regla de administración de firewall"
[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "Regla de RDP de firewall"
[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "Regla web de firewall"
[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "Regla de AppVM01 de firewall"
[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "Regla de salida de firewall"
[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "Regla de DNS de firewall"
[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "Regla entre redes virtuales de firewall"
[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "Regla de denegación de firewall"
[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "Activación de reglas de firewall"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
