los puntos de conexión de Hello enfoque tooAzure funciona un poco distinto entre los modelos de implementación de hello clásico y Administrador de recursos. En el modelo de implementación del Administrador de recursos de hello, ahora dispone de filtros de red de toocreate de flexibilidad de Hola que controlan el flujo de Hola de tráfico dentro y fuera de las máquinas virtuales. Estos filtros le permiten toocreate complejos entornos de red más allá de un punto de conexión simple como en el modelo de implementación de hello clásico. En este artículo se proporciona información general sobre los grupos de seguridad de red y se explican sus diferencias con respecto a los puntos de conexión del modelo clásica, para lo que se crean reglas de filtrado y escenarios de implementación de ejemplo.

## <a name="overview-of-resource-manager-deployments"></a>Información general acerca de las implementaciones de Resource Manager
Puntos de conexión de modelo de implementación clásica de Hola se reemplazan por los grupos de seguridad de red y las reglas de lista (ACL) de control de acceso. Estos son unos rápidos para implementar las reglas de ACL del grupo de seguridad de red:

* Crear un grupo de seguridad de red.
* tooallow o denegar el tráfico, defina las reglas de ACL de grupo de seguridad de red.
* Asignar la interfaz de red de tooa de grupo de seguridad de red o subred de red virtual.

Si desea tooalso realizar el enrutamiento de puerto, que necesita tooplace un equilibrador de carga delante de la máquina virtual y usa las reglas NAT. Estos serían los pasos rápidos para implementar un equilibrador de carga y reglas NAT:

* Cree un equilibrador de carga.
* Cree un grupo back-end y agregue el grupo de toohello de máquinas virtuales.
* Definir las reglas NAT para el reenvío de puerto de hello necesario.
* Asignar las reglas NAT tooyour las máquinas virtuales.

## <a name="network-security-group-overview"></a>Introducción a los grupo de seguridad de red
Grupos de seguridad de red proporcionan un nivel de seguridad para que los puertos específicos de tooallow y subredes tooaccess las máquinas virtuales. Normalmente siempre es necesario proporcionar este nivel de seguridad entre las máquinas virtuales y hello world fuera de un grupo de seguridad de red. Grupos de seguridad de red puede ser aplicada tooa subred de red virtual o una interfaz de red específico para una máquina virtual. En lugar de crear reglas de ACL de punto de conexión, ahora se crean reglas de ACL del grupo de seguridad de red. Estas reglas ACL proporcionan un control mucho mayor que basta con crear un punto de conexión tooforward un puerto determinado. Para más información, consulte [¿Qué es un grupo de seguridad de red?](../articles/virtual-network/virtual-networks-nsg.md)

> [!TIP]
> Puede asignar subredes toomultiple de grupos de seguridad de red o interfaces de red. No hay una asignación 1:1. Puede crear un grupo de seguridad de red con un conjunto común de reglas de ACL y aplicar toomultiple subredes o interfaces de red. Además, el grupo de seguridad de red puede ser tooresources aplicados a través de su suscripción (basado en [controles de acceso en función de rol](../articles/active-directory/role-based-access-control-what-is.md).

## <a name="load-balancers-overview"></a>Información general de los equilibradores de carga
En el modelo de implementación clásica de hello, Azure podría realizar todas las Hola traducción de direcciones de red (NAT) y el puerto reenvío en un servicio de nube para usted. Al crear un punto de conexión, especificaría Hola puerto externo tooexpose junto con hello puerto interno toodirect tráfico. Por sí mismos, los grupos de seguridad de red no realizan el mismo enrutamiento de puertos ni la misma NAT. 

tooallow toocreate reglas NAT para estos puertos de reenvío, creará un equilibrador de carga de Azure en el grupo de recursos. De nuevo, el equilibrador de carga de hello es granular suficiente tooonly aplicar toospecific VM si es necesario. Hello Azure carga trabajo de reglas NAT equilibrador junto con tooprovide de reglas de ACL de grupo de seguridad de red mucha más flexibilidad y control que son posibles con los puntos de conexión de servicio en la nube. Para obtener más información, vea hello [información general del equilibrador de carga](../articles/load-balancer/load-balancer-overview.md).

## <a name="network-security-group-acl-rules"></a>Reglas de ACL del grupo de seguridad de red
Las reglas de ACL permiten definir qué tráfico puede entrar y salir en una máquina virtual en función de determinados puertos, intervalos de puerto o protocolos. Las reglas se asignan tooindividual las máquinas virtuales o subred tooa. Hola siguiente captura de pantalla es un ejemplo de las reglas de ACL para un servidor Web comunes:

![Lista de reglas de ACL del grupo de seguridad de red](./media/virtual-machines-common-endpoints-in-resource-manager/example-acl-rules.png)

Las reglas de ACL se aplican en función de una métrica de prioridad que especifique - Hola mayor sea el valor de hello, menor prioridad de Hola Hola. Cada grupo de seguridad de red tiene el valor predeterminado de tres reglas que están diseñadas toohandle flujo de Hola de tráfico de red de Azure, con explícito `DenyAllInbound` como regla final Hola. Reglas de ACL predeterminada se debido a una prioridad baja toonot interferir con reglas que se crean.

## <a name="assigning-network-security-groups"></a>Asignación de grupos de seguridad de red
Asignar una subred de tooa de grupo de seguridad de red o una interfaz de red. Este enfoque permite toobe tan específicos según sea necesario al aplicar la ACL reglas tooonly una VM específica, o asegurarse de que un conjunto común de ACL reglas son aplicado tooall parte de las máquinas virtuales de una subred:

![Aplicar los NSG toonetwork interfaces o subredes](./media/virtual-machines-common-endpoints-in-resource-manager/apply-nsg-to-resources.png)

comportamiento de Hola de hello grupo de seguridad de red no cambia dependiendo de que se va a asignar tooa subred o una interfaz de red. Un escenario común de implementación tiene Hola que había asignado de grupo de seguridad de red tooa cumplimiento de tooensure de subred de la subred de toothat adjunto de todas las máquinas virtuales. Para obtener más información, consulte [aplicar seguridad de red agrupa tooresources](../articles/virtual-network/virtual-networks-nsg.md#associating-nsgs).

## <a name="default-behavior-of-network-security-groups"></a>Comportamiento predeterminado de grupos de seguridad de red
Dependiendo de cómo y cuándo se cree el grupo de seguridad de red, pueden crearse reglas predeterminadas para el acceso RDP toopermit de máquinas virtuales de Windows en el puerto TCP 3389. Las reglas predeterminadas para las máquinas virtuales Linux permiten el acceso de SSH al puerto TCP 22. Estas reglas ACL automática se crean en hello condiciones siguientes:

* Si crea una VM de Windows a través del portal de Hola y Aceptar Hola predeterminado acción toocreate un grupo de seguridad de red, se crea un ACL regla tooallow el puerto TCP 3389 (RDP).
* Si crea una VM de Linux a través del portal de Hola y Aceptar Hola predeterminado acción toocreate un grupo de seguridad de red, se crea un ACL regla tooallow el puerto TCP 22 (SSH).

Bajo las demás condiciones, estas reglas de ACL predeterminadas no se crean. No se puede conectar tooyour VM sin crear Hola reglas ACL adecuadas. Estas condiciones incluyen hello siguientes acciones comunes:

* Crear un grupo de seguridad de red a través del portal de Hola como un Hola de toocreating acción independiente máquina virtual.
* Creación de un grupo de seguridad de red mediante programación a través de PowerShell, la CLI de Azure, API de REST, etc.
* Crear una máquina virtual y asignarle tooan existente de grupo de seguridad de red que ya no tiene regla ACL adecuada Hola definida.

En Hola a todos los anteriores casos debe toocreate reglas de ACL para las conexiones de administración remota de VM tooallow Hola.

## <a name="default-behavior-of-a-vm-without-a-network-security-group"></a>Comportamiento predeterminado de una máquina virtual sin un grupo de seguridad de red
Es posible crear una máquina virtual sin necesidad de crear un grupo de seguridad de red. En estas situaciones, puede conectarse tooyour VM mediante RDP o SSH sin necesidad de crear cualquier regla de ACL. De forma similar, si se ha instalado un servicio web en el puerto 80, es posible acceder automáticamente a él de forma remota. Hola VM tiene todos los puertos abierto.

> [!NOTE]
> Todavía necesita toohave una tooa de dirección asignada IP virtual pública en orden para cualquier conexión remota. No tener un grupo de seguridad de red para la interfaz de red o de subred de hello no expone tráfico externo de hello VM tooany. acción de Hello predeterminada al crear una máquina virtual a través del portal de hello es toocreate una IP pública nueva. En el caso de las demás formas de crear una máquina virtual como PowerShell, la CLI de Azure o una plantilla de Resource Manager, no se crea automáticamente una dirección IP pública, a menos que se solicite explícitamente. acción predeterminada de Hola a través del portal de hello también es toocreate un grupo de seguridad de red. Esta acción predeterminada significa que no debe terminar en una situación con una máquina virtual expuesta que no tenga el filtrado de redes instalado.

## <a name="understanding-load-balancers-and-nat-rules"></a>Descripción de las reglas NAT y los equilibradores de carga
En el modelo de implementación de hello clásico, puede crear puntos de conexión que también realizan el reenvío de puerto. Cuando se crea una máquina virtual en el modelo de implementación clásica de hello, se crearán automáticamente las reglas de ACL para RDP o SSH. Estas reglas no expondría el puerto TCP 3389 o el puerto TCP 22 respectivamente toohello fuera del mundo. En su lugar, podría exponerse un puerto TCP de gran valor que se asigna un puerto interno toohello adecuado. También puede crear sus propias reglas ACL de forma similar, como exponer un webserver en TCP puerto 4280 toohello fuera del mundo. Puede ver estas reglas ACL y las asignaciones de puerto en hello siguiendo la captura de pantalla de portal clásico de hello:

![Enrutamiento de puertos con punto de conexión del modelo de implementación Clásico](./media/virtual-machines-common-endpoints-in-resource-manager/classic-endpoints-port-forwarding.png)

Con los grupos de seguridad de red, la función de enrutamiento de puertos la controla un equilibrador de carga. Para más información, consulte los [equilibradores de carga de Azure](../articles/load-balancer/load-balancer-overview.md). Hello en el ejemplo siguiente se muestra un equilibrador de carga con una NAT regla tooperform reenvío de puerto TCP puerto 4222 toohello interno el puerto TCP 22 una máquina virtual:

![Reglas NAT del equilibrador para el enrutamiento de puertos](./media/virtual-machines-common-endpoints-in-resource-manager/load-balancer-nat-rules.png)

> [!NOTE]
> Al implementar un equilibrador de carga, por lo general no asigna Hola propia máquina virtual una dirección IP pública. En su lugar, equilibrador de carga de hello tiene un tooit dirección asignada de IP pública. Todavía necesita toocreate el grupo de seguridad de red y ACL reglas toodefine Hola el flujo de tráfico dentro y fuera de la máquina virtual. Hello las reglas NAT de equilibrador de carga son simplemente toodefine los puertos que se permiten a través del equilibrador de carga de Hola y cómo obtener distribuyen a través de back-end de hello las máquinas virtuales. Por lo tanto, necesitará toocreate una regla NAT para tráfico tooflow a través del equilibrador de carga de Hola. tooallow Hola tráfico tooreach Hola VM, cree una regla de ACL de grupo de seguridad de red.
