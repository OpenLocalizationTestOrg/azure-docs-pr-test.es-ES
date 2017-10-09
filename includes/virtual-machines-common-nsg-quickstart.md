Abrir un puerto, o crear un punto de conexión, tooa máquina virtual (VM) de Azure mediante la creación de un filtro de red en una subred o una interfaz de red de máquina virtual. Estos filtros, que controlan el tráfico entrante y saliente, se coloca en un recurso de grupo de seguridad de red conectado toohello que recibe el tráfico de Hola.

Vamos a usar un ejemplo común de tráfico web en el puerto 80. Una vez que tenga una máquina virtual que está configurado tooserve web solicitudes en el puerto estándar de TCP 80 hello (recuerde servicios apropiados de toostart hello y abrir las reglas de firewall de SO en hello VM),:

1. Crear un grupo de seguridad de red.
2. Crear una regla de entrada que permita el tráfico con la siguiente configuración:
   * intervalo de puertos de destino de Hola de "80"
   * Hola intervalo de puertos de origen de "*" (lo que permite cualquier puerto de origen)
   * un valor de prioridad de menos 65.500 (toobe situado más arriba en la prioridad de hello catch de forma predeterminada, todo ello denegar regla de entrada)
3. Asociar Hola grupo de seguridad de red con la interfaz de red VM de Hola o subred.

Puede crear toosecure de configuraciones de red compleja su entorno mediante reglas y grupos de seguridad de red. Nuestro ejemplo solo utiliza una o dos reglas que permiten el tráfico HTTP o la administración remota. Para obtener más información, vea el siguiente hello [obtener más información](#more-information-on-network-security-groups) sección o [¿qué es un grupo de seguridad de red?](../articles/virtual-network/virtual-networks-nsg.md)

