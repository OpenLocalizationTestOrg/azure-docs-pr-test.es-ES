## <a name="sample-scenario"></a>Escenario de ejemplo
toobetter ilustran cómo toomanage NSG, este artículo usa escenario hello más adelante.

![Escenario de red virtual](./media/virtual-networks-create-nsg-scenario-include/figure1.png)

En este escenario creará un NSG para cada subred Hola **TestVNet** red virtual, tal como se describe a continuación: 

* **NSG-FrontEnd**. Hello front-end NSG será aplicado toohello *front-end* subred y contienen dos reglas:    
  * **rdp-rule**. Esta regla permitirá toohello de tráfico RDP *front-end* subred.
  * **web-rule**. Esta regla permitirá toohello de tráfico HTTP *front-end* subred.
* **NSG-BackEnd**. back-end de Hello NSG será aplicado toohello *back-end* subred y contienen dos reglas:    
  * **sql-rule**. Esta regla permite el tráfico SQL sólo desde hello *front-end* subred.
  * **web-rule**. Esta regla deniega el tráfico saliente de internet todos de hello *back-end* subred.

combinación de Hola de estas reglas crear un escenario similar de la red Perimetral, donde sólo puede recibir tráfico entrante para el tráfico SQL de la subred de front-end de hello subred de back-end de Hola y no tiene ningún toohello de acceso a Internet, mientras que la subred de front-end de hello puede comunicarse con hello Internet y recibir sólo las solicitudes HTTP entrantes.

escenario de hello toodeploy descrita anteriormente, siga [este vínculo](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), haga clic en **implementar tooAzure**, reemplazar valores de parámetro predeterminados de hello si es necesario y siga las instrucciones de hello del portal de Hola. En las instrucciones de ejemplo de Hola a continuación, la plantilla de hello era toodeploy usa un recurso de nombres de grupos de **NSG RG**. 

