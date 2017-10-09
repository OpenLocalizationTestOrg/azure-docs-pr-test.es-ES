## <a name="how-toocreate-a-classic-vnet-using-azure-cli"></a>¿Cómo toocreate una red virtual clásica con CLI de Azure
Puede usar hello Azure CLI toomanage los recursos de Azure Hola desde línea de comandos desde cualquier equipo que ejecute Windows, Linux y OSX. toocreate una red virtual mediante el uso de hello CLI de Azure, siga estos pasos Hola.

1. Si nunca ha utilizado la CLI de Azure, consulte [instalar y configurar hello Azure CLI](../articles/cli-install-nodejs.md) y siga las instrucciones de hello punto toohello donde seleccionar su cuenta de Azure y la suscripción.
2. Ejecute hello **crear red virtual de red de azure** comandos toocreate una red virtual y una subred, tal y como se muestra a continuación. lista de Hola que se muestra después de la salida de hello explica parámetros Hola utilizados.
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    Resultado esperado:
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * **--vnet**. Nombre de hello toobe de red virtual creado. En este escenario, *TestVNet*
   * **-e (o --address-space)**. Espacio de direcciones de red virtual. En este escenario, *192.168.0.0*
   * **-i (o -cidr)**. Máscara de red en formato CIDR. En este escenario, *16*.
   * **-n (o --subnet-name**). Nombre de la primera subred de Hola. En este escenario, *FrontEnd*.
   * **-p (or --subnet-start-ip)**. Dirección IP inicial de la subred o el espacio de direcciones de la subred. En este escenario, *192.168.1.0*.
   * **-r (o --subnet-cidr)**. Máscara de red en formato CIDR para subred. En este escenario, *24*.
   * **-l (o --location)**. Región de Azure donde se creará Hola red virtual. En este escenario, *Central US*.
3. Ejecute hello **crear subredes de red virtual de red de azure** comando toocreate una subred tal y como se muestra a continuación. lista de Hola que se muestra después de la salida de hello explica parámetros Hola utilizados.
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    Este es el resultado de hello esperada en comando hello anterior:
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * **-t (o --vnet-name**. Nombre de red virtual donde se creará la subred de Hola Hola. En este escenario, *TestVNet*.
   * **-n (o --name)**. Nombre de subred nueva Hola. En este escenario, *BackEnd*.
   * **-a (or --address-prefix)**. Bloque CIDR de subred. En este escenario, *192.168.2.0/24*.
4. Ejecute hello **mostrar de la red virtual de red de azure** comando Propiedades de hello tooview de red virtual nueva hello, tal y como se muestra a continuación.
   
            azure network vnet show
   
    Este es el resultado de hello esperada en comando hello anterior:
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

