## <a name="scenario"></a>Escenario
toobetter ilustran cómo toocreate NSG, este documento empleará escenario hello más adelante.

![Escenario de red virtual](./media/virtual-networks-create-nsg-scenario-include/figure1.png)

En este escenario creará un NSG para cada subred Hola **TestVNet** red virtual, tal como se describe a continuación: 

* **NSG-FrontEnd**. Hello front-end NSG será aplicado toohello *front-end* subred y contienen dos reglas:    
  * **rdp-rule**. Esta regla permitirá toohello de tráfico RDP *front-end* subred.
  * **web-rule**. Esta regla permitirá toohello de tráfico HTTP *front-end* subred.
* **NSG-BackEnd**. back-end de Hello NSG será aplicado toohello *back-end* subred y contienen dos reglas:    
  * **sql-rule**. Esta regla permite el tráfico SQL sólo desde hello *front-end* subred.
  * **web-rule**. Esta regla deniega el tráfico saliente de internet todos de hello *back-end* subred.

combinación de estas reglas Hello crear un escenario similar de la red Perimetral, donde subred de back-end de hello solo puede recibir tráfico entrante para SQL de la subred de front-end de Hola y no tiene ningún toohello de acceso a Internet, mientras la subred de front-end de hello puede comunicarse con hello Internet, y recibir sólo las solicitudes HTTP entrantes.

