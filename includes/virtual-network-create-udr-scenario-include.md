## <a name="scenario"></a>Escenario
toobetter ilustran cómo toocreate UDRs, este documento empleará escenario hello más adelante.

![DESCRIPCIÓN DE LA IMAGEN](./media/virtual-network-create-udr-scenario-include/figure1.png)

En este escenario creará un UDR para hello *subred de Front end* y otra UDR para hello *subred de Back end* , tal y como se describe a continuación: 

* **UDR-FrontEnd**. Hello front-end UDR será aplicado toohello *front-end* subred y contener una ruta:    
  * **RouteToBackend**. Esta ruta enviará todos los toohello de subred back-end de tráfico toohello **FW1** máquina virtual.
* **UDR-BackEnd**. back-end de Hello UDR será aplicado toohello *back-end* subred y contener una ruta:    
  * **RouteToFrontend**. Esta ruta enviará todos los toohello de subred front-end de tráfico toohello **FW1** máquina virtual.

combinación de Hola de estas rutas se asegurará de que todo el tráfico destinado de un tooanother de subred será enrutado toohello **FW1** máquina virtual, que se usa como un dispositivo virtual. También deberá tooturn de reenvío IP para esa máquina virtual, tooensure pueda recibir el tráfico destinado tooother las máquinas virtuales.

