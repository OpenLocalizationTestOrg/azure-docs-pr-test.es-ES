## <a name="scenario"></a>Escenario
toobetter ilustran cómo toocreate una red virtual y subredes, este documento se empleará escenario hello más adelante.

![Escenario de red virtual](./media/virtual-networks-create-vnet-scenario-include/vnet-scenario.png)

En este escenario, creará una red virtual denominada **TestVNet** con un bloque CIDR reservado de **192.168.0.0./16**. La red virtual contendrá Hola siguientes: 

* **FrontEnd**, con **192.168.1.0/24** como su bloque CIDR.
* **BackEnd**, con **192.168.2.0/24** como su bloque CIDR.

