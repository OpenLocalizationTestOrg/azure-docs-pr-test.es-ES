Si tiene problemas para conectarse a máquina virtual de tooa a través de la conexión VPN, compruebe Hola siguiente:

- Compruebe que la conexión VPN se ha establecido correctamente.
- Compruebe que se está conectando toohello dirección IP privada Hola máquina virtual.
- Si se puede conectar toohello VM con IP privada Hola de direcciones, pero no Hola nombre de equipo, compruebe que ha configurado DNS correctamente. Para más información acerca de cómo funciona la resolución de nombres para las máquinas virtuales, consulte [Resolución de nombres para las máquinas virtuales e instancias de rol](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

Cuando se conecta a través de Point-to-Site, compruebe Hola siguientes elementos adicionales:

- Use 'ipconfig' toocheck Hola dirección IPv4 asignada a toohello adaptador de Ethernet en el equipo Hola desde el que se va a conectar. Si dirección IP de hello es dentro del intervalo de direcciones de Hola de hello red virtual que se está conectando a o dentro del intervalo de direcciones de Hola de su VPNClientAddressPool, esto es tooas que se hace referencia un espacio de direcciones superpuestos. Cuando se solapa con el espacio de direcciones de esta manera, el tráfico de red hello no llegar a Azure, se mantiene en la red local de Hola.
- Compruebe que se generó ese paquete de configuración de cliente VPN de hello después de que se especificaron direcciones IP del servidor DNS de Hola para hello red virtual. Si ha actualizado de direcciones IP del servidor DNS de hello, generar e instalar un nuevo paquete de configuración de cliente VPN.

Para obtener más información sobre cómo solucionar problemas de una conexión RDP, consulte [tooa de conexiones de escritorio remoto solucionar VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).
