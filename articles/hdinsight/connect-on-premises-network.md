---
title: red de local tooyour aaaConnect HDInsight - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una HDInsight de clúster en una red Virtual de Azure y, a continuación, conéctelo red de tooyour local. Obtenga información acerca de cómo tooconfigure resolución de nombres entre HDInsight y la red local mediante el uso de un servidor DNS personalizado."
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a3adf0e3df7726d8e6566d723700506baaf89a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-hdinsight-tooyour-on-premise-network"></a>Conectar HDInsight tooyour en la red local

Obtenga información acerca de cómo tooconnect HDInsight tooyour en local de red mediante redes virtuales de Azure y una puerta de enlace VPN. En este documento se brinda información de planeación sobre:

* Uso de HDInsight en una red Virtual de Azure que se conecta tooyour local de red.

* Configuración de resolución de nombres DNS entre la red virtual de Hola y de la red local.

* Configuración de red seguridad grupos toorestrict internet acceso tooHDInsight.

* Puertos proporcionados por HDInsight en la red virtual de Hola.

## <a name="create-hello-virtual-network-configuration"></a>Crear configuración de red Virtual de Hola

> [!IMPORTANT]
> Si desea obtener instrucciones paso a paso sobre cómo conectar HDInsight tooyour local de red mediante una red Virtual de Azure, vea hello [HDInsight conectar tooyour en la red local](connect-on-premises-network.md) documento.

Siguiente Hola de uso documenta toolearn cómo toocreate una red Virtual de Azure que está conectado tooyour local red:
    
* [Uso de hello portal de Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [Uso de Azure PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [Uso de la CLI de Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a>Configuración de la resolución de nombres

tooallow HDInsight y recursos de hello unido red toocommunicate por su nombre, debe realizar Hola siguientes acciones:

* Crear un servidor DNS personalizado en hello red Virtual de Azure.

* Configurar Hola red virtual toouse Hola servidor DNS personalizado en lugar de forma predeterminada Hola resolución recursiva de Azure.

* Configure el enrutamiento entre servidores DNS personalizados de Hola y el servidor DNS local.

Esta configuración permite Hola siguiente comportamiento:

* Las solicitudes de nombres de dominio completo que tienen el sufijo DNS de hello __para la red virtual de hello__ se reenvían toohello servidor DNS personalizado. servidor DNS personalizado de Hello, a continuación, reenvía estos toohello solicitudes resolución recursiva de Azure, que devuelve la dirección IP de Hola.

* Todas las demás solicitudes se reenvían a servidor DNS local toohello. Incluso las solicitudes para recursos de internet pública como microsoft.com se reenvían toohello servidor DNS local para la resolución de nombres.

Hola siguiente diagrama, líneas verdes son solicitudes para recursos que terminen en el sufijo DNS de Hola de red virtual de Hola. Líneas azules son solicitudes para recursos en la red local de Hola o en Hola internet pública.

![Diagrama de cómo se resuelven las solicitudes DNS en la configuración de hello usado en este documento](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a>Creación de un servidor DNS personalizado

> [!IMPORTANT]
> Debe crear y configurar el servidor DNS de hello antes de instalar HDInsight en la red virtual de Hola.

una VM de Linux que usa hello toocreate [enlazar](https://www.isc.org/downloads/bind/) software DNS, Hola uso pasos:

> [!NOTE]
> pasos siguientes Hello utilizan hello [portal de Azure](https://portal.azure.com) toocreate máquinas virtuales de Azure. Para otro toocreate formas una máquina virtual, vea hello [crear VM - Azure CLI](../virtual-machines/linux/quick-create-cli.md) y [crear VM - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documentos.

1. De hello [portal de Azure](https://portal.azure.com), seleccione  __+__ , __proceso__, y __Ubuntu Server 16.04 LTS__.

    ![Creación de una máquina virtual Ubuntu](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. De hello __Fundamentos__ sección, escriba Hola siguiente información:

    * __Nombre__: nombre descriptivo que identifica esta máquina virtual. Por ejemplo, __DNSProxy__.
    * __Nombre de usuario__: nombre de Hola de hello cuenta SSH.
    * __Clave pública SSH__ o __contraseña__: Hola método de autenticación para hello cuenta SSH. Se recomienda usar claves públicas, porque son más seguras. Para obtener más información, vea hello [crear y usar claves SSH para máquinas virtuales Linux](../virtual-machines/linux/mac-create-ssh-keys.md) documento.
    * __Grupo de recursos__: seleccione __utilizar existente__y, a continuación, seleccione grupo de recursos de Hola que contiene Hola red virtual que creó anteriormente.
    * __Ubicación__: seleccione Hola la misma ubicación que la red virtual de Hola.

    ![Configuración básica de la máquina virtual](./media/connect-on-premises-network/vm-basics.png)

    Deje las demás entradas en hello valores predeterminados y, a continuación, seleccione __Aceptar__.

3. De hello __elegir un tamaño de__ sección, tamaño de máquina virtual de hello select. Para este tutorial, seleccione hello más pequeño y opción de costo más bajo. toocontinue, use hello __seleccione__ botón.

4. De hello __configuración__ sección, escriba Hola siguiente información:

    * __Red virtual__: seleccione Hola red virtual que creó anteriormente.

    * __Subred__: seleccione subred predeterminada de hello para la red virtual de Hola. Hacer __no__ seleccione Hola subred usada por la puerta de enlace VPN de Hola.

    * __Cuenta de almacenamiento de diagnóstico__: seleccione una cuenta de almacenamiento existente o cree una nueva.

    ![Configuración de la red virtual](./media/connect-on-premises-network/virtual-network-settings.png)

    Deje las demás entradas de Hola como valor predeterminado de hello, a continuación, seleccione __Aceptar__ toocontinue.

5. De hello __compra__ sección, seleccione hello __compra__ máquina virtual de botón toocreate Hola.

6. Una vez creada la máquina virtual de hello, su __Introducción__ sección se muestra. En la lista Hola Hola izquierda, seleccione __propiedades__. Guardar hello __dirección IP pública__ y __dirección IP privada__ valores. Se utilizará en la sección siguiente Hola.

    ![Direcciones IP pública y privada](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a>Instalación y configuración de Bind (software DNS)

1. Utilizar SSH tooconnect toohello __dirección IP pública__ de máquina virtual de Hola. Hola siguiente ejemplo conecta a máquina virtual de tooa en 40.68.254.142:

    ```bash
    ssh sshuser@40.68.254.142
    ```

    Reemplace `sshuser` con hello cuenta de usuario SSH que especificó al crear el clúster de Hola.

    > [!NOTE]
    > Hay una variedad de Hola de formas tooobtain `ssh` utilidad. En Linux, Unix y macOS, se proporciona como parte del sistema operativo de Hola. Si usas Windows, considere una de las siguientes opciones de hello:
    >
    > * [Azure Cloud Shell](../cloud-shell/quickstart.md)
    > * [Bash en Ubuntu en Windows 10](https://msdn.microsoft.com/commandline/wsl/about)
    > * [GIT (https://git-scm.com/)](https://git-scm.com/)
    > * [OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. tooinstall Bind, utilice Hola siga los comandos de la sesión de SSH de hello:

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. tooconfigure tooforward nombre resolución solicitudes tooyour local DNS servidor Bind, usar hello después de texto como contenido de Hola de hello `/etc/bind/named.conf.options` archivo:

        acl goodclients {
            10.0.0.0/16; # Replace with hello IP address range of hello virtual network
            10.1.0.0/16; # Replace with hello IP address range of hello on-premises network
            localhost;
            localnets;
        };

        options {
                directory "/var/cache/bind";

                recursion yes;

                allow-query { goodclients; };

                forwarders {
                192.168.0.1; # Replace with hello IP address of hello on-premises DNS server
                };

                dnssec-validation auto;

                auth-nxdomain no;    # conform tooRFC1035
                listen-on { any; };
        };

    > [!IMPORTANT]
    > Reemplace los valores de hello en hello `goodclients` sección con el intervalo de direcciones IP de Hola de red virtual de Hola y red local. Esta sección define las direcciones de Hola que este servidor DNS acepta solicitudes de.
    >
    > Reemplace hello `192.168.0.1` entrada Hola `forwarders` sección con la dirección IP de saludo del servidor DNS local. Esta tooyour de las solicitudes de entrada rutas DNS local de servidor DNS para la resolución.

    tooedit este archivo, Hola de uso siguiente comando:

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    archivo de hello toosave, use __CTRL+x__, __Y__y, a continuación, __ENTRAR__.

4. Desde la sesión de SSH de hello, use Hola siguiente comando:

    ```bash
    hostname -f
    ```

    Este comando devuelve un toohello similar valor siguiente texto:

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    Hola `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` texto es hello __sufijo DNS__ para esta red virtual. Guarde este valor, porque se usará más adelante.

5. Enlace de nombres DNS tooconfigure tooresolve para los recursos de red virtual de hello, usar hello después de texto como contenido de Hola de hello `/etc/bind/named.conf.local` archivo:

        // Replace hello following with hello DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # hello Azure recursive resolver
        };

    > [!IMPORTANT]
    > Debe reemplazar hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` con el sufijo DNS de hello recuperó anteriormente.

    tooedit este archivo, Hola de uso siguiente comando:

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    archivo de hello toosave, use __CTRL+x__, __Y__y, a continuación, __ENTRAR__.

6. toostart Bind, utilice Hola siguiente comando:

    ```bash
    sudo service bind9 restart
    ```

7. tooverify que enlazan puede resolver los nombres de Hola de recursos de la red local, Hola de uso después de comandos:

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > Reemplace `dns.mynetwork.net` con el nombre de dominio completo (FQDN) de Hola de un recurso en la red local.
    >
    > Reemplace `10.0.0.4` con hello __dirección IP interna__ del servidor DNS personalizado en la red virtual de Hola.

    respuesta de Hola aparece toohello similar siguiente texto:

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-hello-virtual-network-toouse-hello-custom-dns-server"></a>Configurar servidor DNS personalizado de hello red virtual toouse Hola

tooconfigure Hola red virtual toouse Hola servidor DNS personalizado en lugar de hello resolución recursiva de Azure, use Hola siguiendo los pasos:

1. Hola [portal de Azure](https://portal.azure.com), seleccione la red virtual de hello y, a continuación, seleccione __servidores DNS__.

2. Seleccione __personalizado__y escriba hello __dirección IP interna__ del servidor DNS personalizado Hola. Por último, seleccione __Guardar__.

    ![Servidor DNS conjunto Hola personalizado para la red de Hola](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-hello-on-premises-dns-server"></a>Configurar servidor DNS local Hola

En la sección anterior de hello, configuró Hola personalizado DNS server tooforward solicitudes toohello en servidor DNS local. A continuación, debe configurar hello en DNS server tooforward solicitudes toohello personalizado servidor DNS local.

Para obtener pasos específicos sobre cómo tooconfigure el servidor DNS, consulte la documentación de hello para el software del servidor DNS. Busque los pasos hello tooconfigure una __reenviador condicional__.

Un reenvío condicional solo reenvía solicitudes para un sufijo DNS específico. En este caso, debe configurar un reenviador para el sufijo DNS de Hola de red virtual de Hola. Se deberían reenviar las solicitudes de este sufijo toohello dirección IP del servidor DNS personalizado de Hola. 

Hello texto siguiente es un ejemplo de una configuración de reenviador condicional para hello **enlazar** software DNS:

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello custom DNS server's internal IP address
    };

Para obtener información sobre el uso de DNS en **Windows Server 2016**, vea hello [DnsServerConditionalForwarderZone agregar](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentación...

Una vez haya configurado el servidor DNS de hello en local, puede utilizar `nslookup` de tooverify de red local de Hola que pueda resolver los nombres de red virtual de Hola. Hola siguiente ejemplo 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

Este ejemplo usa Hola servidor DNS local en 196.168.0.4 tooresolve Hola nombre de saludo personalizado servidor DNS. Reemplace la dirección IP de hello con hello para el servidor DNS local Hola. Reemplace hello `dnsproxy` dirección con el nombre de dominio completo de Hola de servidor DNS personalizado de Hola.

## <a name="optional-control-network-traffic"></a>Opcional: control del tráfico de red

Puede usar grupos de seguridad de red (NSG) o el tráfico de red de rutas definidas por el usuario (UDR) toocontrol. Los NSG permiten toofilter entrantes y salientes de tráfico y permitir o denegar el tráfico de Hola. UDRs le permiten toocontrol cómo fluye el tráfico entre los recursos de red virtual de hello, Hola internet y Hola red local.

> [!WARNING]
> HDInsight requiere acceso de entrada desde direcciones IP específicas en la nube de Azure de Hola y sin restricciones de acceso de salida. Cuando se utiliza el tráfico de toocontrol NSG o UDRs, debe realizar Hola pasos:
>
> 1. Encontrar Hola direcciones IP para la ubicación de Hola que contiene la red virtual. Para obtener una lista de las direcciones IP requeridas por ubicación, consulte [Direcciones IP requeridas](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).
>
> 2. Permitir el tráfico entrante desde direcciones IP de Hola.
>
>    * __NSG__: permitir __entrada__ tráfico en el puerto __443__ de hello __Internet__.
>    * __UDR__: Hola conjunto __próximo salto__ tipo de hello ruta too__Internet__.

Para obtener un ejemplo del uso de Azure PowerShell o CLI de Azure de hello toocreate NSG, vea hello [HDInsight ampliar con redes virtuales de Azure](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) documento.

## <a name="create-hello-hdinsight-cluster"></a>Crear el clúster de HDInsight de Hola

> [!WARNING]
> Debe configurar el servidor DNS personalizado de hello antes de instalar HDInsight en la red virtual de Hola.

Hola de uso de los pasos de hello [crear un clúster de HDInsight mediante Hola portal de Azure](./hdinsight-hadoop-create-linux-clusters-portal.md) documento toocreate un clúster de HDInsight.

> [!WARNING]
> * Durante la creación del clúster, debe elegir ubicación de Hola que contiene la red virtual.
>
> * Hola __configuración avanzada__ parte de configuración, debe seleccionar la red virtual de Hola y de las subredes que creó anteriormente.

## <a name="connecting-toohdinsight"></a>Conexión tooHDInsight

Documentación mayoría en HDInsight se da por supuesto que tiene acceso toohello clúster sobre Hola internet. Por ejemplo, que se puede conectar el clúster de toohello en https://CLUSTERNAME.azurehdinsight.net. Esta dirección utiliza la puerta de enlace pública hello, que no está disponible si ha usado NSG u Hola a UDRs toorestrict acceso desde internet.

toodirectly conecte tooHDInsight a través de la red virtual de hello, usar hello pasos:

1. nombres de dominio completo interno de hello toodiscover de nodos de clúster de HDInsight de hello, use uno de los siguientes métodos de hello:

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

2. puerto de hello toodetermine que un servicio está disponible en, vea hello [puertos utilizados por los servicios de Hadoop en HDInsight](./hdinsight-hadoop-port-settings-for-services.md) documento.

    > [!IMPORTANT]
    > Algunos servicios hospedados en nodos principales Hola sólo están activas en un nodo a la vez. Si intenta obtener acceso a un servicio en un nodo principal y se produce un error, cambie toohello otro nodo principal.
    >
    > Por ejemplo, Ambari solo está activo en un nodo principal a la vez. Si intenta tener acceso a Ambari en un nodo principal y devuelve un error 404, a continuación, se ejecuta en Hola otro nodo principal.

## <a name="next-steps"></a>Pasos siguientes

* Para más información sobre cómo usar HDInsight en una red virtual, vea [Extensión de las funcionalidades de HDInsight con Red virtual de Azure](./hdinsight-extend-hadoop-virtual-network.md).

* Para obtener más información sobre redes virtuales de Azure, vea hello [información general de la red Virtual de Azure](../virtual-network/virtual-networks-overview.md).

* Para más información sobre los grupos de seguridad de red, vea [Grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md).

* Para más información sobre las rutas definidas por el usuario, vea [Rutas definidas por el usuario y reenvío IP](../virtual-network/virtual-networks-udr-overview.md).
