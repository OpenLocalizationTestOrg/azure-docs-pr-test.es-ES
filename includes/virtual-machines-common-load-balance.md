

Hay dos niveles de equilibrio de carga disponibles para Servicios de infraestructura de Azure:

* **Nivel de DNS**: equilibrio de carga para servicios en la nube de tráfico toodifferent ubicados en datos diferentes centros, toodifferent sitios Web de Azure ubicados en distintos centros de datos, o tooexternal los puntos de conexión. Esto se hace con el Administrador de tráfico de Azure y método de equilibrio de carga de hello Round Robin.
* **Nivel de red**: equilibrio de carga de entrada Internet tráfico toodifferent máquinas virtuales a de un servicio de nube o el equilibrio de carga de tráfico entre máquinas virtuales en un servicio en la nube o red virtual. Esto se realiza con el equilibrador de carga de Azure Hola.

## <a name="traffic-manager-load-balancing-for-cloud-services-and-websites"></a>Equilibrio de carga del Administrador de tráfico para servicios en la nube y sitios web
Traffic Manager permite la distribución de hello toocontrol de tooendpoints de tráfico de usuario, que pueden incluir servicios en la nube, sitios Web, sitios externos y otros perfiles de Traffic Manager. Traffic Manager funciona aplicando un consultas de sistema de nombres (DNS) de directivas inteligente motor tooDomain Hola nombres de dominio de los recursos de Internet. Los servicios en la nube o sitios Web puede ejecutarse en distintos centros de datos a través de Hola a todos.

Debe usar REST o Windows PowerShell extremos externos tooconfigure o perfiles de administrador de tráfico como extremos.

Administrador de tráfico usa tres tráfico de toodistribute de métodos de equilibrio de carga:

* **Conmutación por error**: Utilice este método cuando desee toouse un extremo principal para todo el tráfico, pero proporcionar copias de seguridad en caso de hello principal deja de estar disponible.
* **Rendimiento**: Utilice este método cuando tenga extremos en diferentes ubicaciones geográficas y desee solicitar clientes toouse Hola "más cercano" punto de conexión en términos de latencia más baja de Hola.
* **Operación por turnos:** Utilice este método cuando desee toodistribute carga a través de un conjunto de nube de servicios en hello mismo centro de datos o a través de servicios en la nube o sitios Web en distintos centros de datos.

Para más información, consulte [Métodos de enrutamiento de tráfico de Traffic Manager](../articles/traffic-manager/traffic-manager-routing-methods.md).

Hola siguiente diagrama muestra un ejemplo de Hola método de equilibrio de carga Round Robin para distribuir el tráfico entre servicios en la nube diferente.

![equilibrio de carga](./media/virtual-machines-common-load-balance/TMSummary.png)

proceso básico de Hello es siguiente de hello:

1. Un cliente de Internet consulta un servicio nombres de dominio correspondientes tooa web.
2. DNS reenvía tooTraffic Manager de la solicitud de consulta del nombre hello.
3. Administrador de tráfico elige Hola siguiente servicio en la nube en la lista de operación por turnos de Hola y le responde Hola nombre DNS. servidor DNS del cliente de Internet de Hello resuelve la dirección IP de hello nombre tooan y envía al cliente de Internet toohello.
4. cliente de Internet de Hola se conecta con el servicio de nube de hello elegido por el Administrador de tráfico.

Para obtener más información, consulte [Administrador de tráfico](../articles/traffic-manager/traffic-manager-overview.md).

## <a name="azure-load-balancing-for-virtual-machines"></a>Equilibrio de carga de Azure para máquinas virtuales
Hola de máquinas virtuales en el mismo servicio en la nube o red virtual puede comunicarse entre sí directamente mediante sus direcciones IP privadas. Servicio de nube de equipos y servicios fuera de Hola o red virtual sólo puede comunicarse con máquinas virtuales en un servicio en la nube o red virtual con un punto de conexión configurado. Un punto de conexión es una asignación de una dirección IP pública y la dirección IP privada de toothat del puerto y el puerto de una máquina virtual o el rol web dentro de un servicio de nube de Azure.

Hola equilibrador de carga de Azure distribuye aleatoriamente un tipo específico de tráfico entrante entre varias máquinas virtuales o servicios en una configuración que se conoce como un conjunto de equilibrio de carga. Por ejemplo, se puede propagar carga Hola de tráfico de solicitudes web en varios servidores web o roles web.

Hello siguiente diagrama muestra un extremo con equilibrio de carga para tráfico de web (sin cifrar) estándar que se comparte entre tres máquinas virtuales para hello pública y privada puerto TCP 80. Estas tres máquinas virtuales se encuentran en un conjunto con equilibrio de carga.

![equilibrio de carga](./media/virtual-machines-common-load-balance/LoadBalancing.png)

Para obtener más información, consulte [Equilibrador de carga de Azure](../articles/load-balancer/load-balancer-overview.md). Para los pasos de hello toocreate un conjunto de equilibrio de carga, consulte [configurar un conjunto con equilibrio de carga](../articles/load-balancer/load-balancer-get-started-internet-arm-ps.md).

Azure también puede equilibrar la carga en un servicio en la nube o una red virtual. Esto se conoce como Equilibrio de carga interno y puede utilizarse en hello siguientes maneras:

* saldo de tooload entre los servidores de distintos niveles de una aplicación de varios niveles (por ejemplo, entre las capas web y de base de datos).
* tooload equilibrar la línea de negocio (LOB) las aplicaciones hospedadas en Azure sin necesidad de software o hardware de equilibrador de carga adicional.
* tooinclude servidores locales en conjunto de Hola de equipos cuyo tráfico tiene equilibrada de carga.

Similar tooAzure equilibrio de carga, equilibrio de carga interno se facilita mediante la configuración de un conjunto de equilibrio de carga interno.

Hola siguiente diagrama muestra un ejemplo de un extremo con equilibrio de carga interno para una aplicación de línea de negocio (LOB) que se comparte entre tres máquinas virtuales en una red virtual entre entornos.

![equilibrio de carga](./media/virtual-machines-common-load-balance/LOBServers.png)

## <a name="load-balancer-considerations"></a>Consideraciones sobre el equilibrador de carga
Un equilibrador de carga se configura de forma predeterminada tootimeout una sesión inactiva en 4 minutos. Si la aplicación detrás de un equilibrador de carga sale de una conexión inactiva durante más de 4 minutos y no tiene una configuración Keep-Alive, conexión Hola se van a quitar. Puede cambiar tooallow de comportamiento de equilibrador de carga de hello un [más configuración de tiempo de espera para el equilibrador de carga de Azure de](../articles/load-balancer/load-balancer-tcp-idle-timeout.md).

Otra consideración es tipo hello del modo de distribución compatible con el equilibrador de carga de Azure. Puede configurar la afinidad de dirección IP de origen (dirección de IP de origen, dirección IP de destino) o el protocolo IP de origen (dirección IP de origen, protocolo y dirección IP de destino). Revise el [modo de distribución del equilibrador de carga de Azure (afinidad de dirección IP de origen)](../articles/load-balancer/load-balancer-distribution-mode.md) para más información.

## <a name="next-steps"></a>Pasos siguientes
Para los pasos de hello toocreate un conjunto de equilibrio de carga, consulte [configurar un conjunto de equilibrio de carga interno](../articles/load-balancer/load-balancer-get-started-ilb-arm-ps.md).

Para obtener más información, consulte [Equilibrio de carga interno](../articles/load-balancer/load-balancer-internal-overview.md).

