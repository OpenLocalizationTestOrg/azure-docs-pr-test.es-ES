Puede conectarse tooa máquina virtual que está implementado tooyour red virtual mediante la creación de una máquina virtual tooyour de conexión a Escritorio remoto. Hello tooinitially de mejor manera comprueba que puedes conectarte tooyour VM es tooconnect por utilizar IP privadas de su dirección, en lugar del nombre del equipo. De este modo, se prueban por toosee si puede conectarse, no si la resolución de nombres está configurada correctamente. 

1. Busque la dirección IP privada de hello para la máquina virtual. Puede encontrar la dirección IP privada de Hola de una máquina virtual examinando propiedades Hola Hola VM Hola portal de Azure, o mediante PowerShell.
2. Compruebe que está conectado tooyour red virtual con hello Point-to-Site VPN conexión. 
3. Abrir conexión a Escritorio remoto, escriba "RDP" o "Conexión a Escritorio remoto" en el cuadro de búsqueda de hello en la barra de tareas de hello, a continuación, seleccione la conexión a Escritorio remoto. También puede abrir conexión a Escritorio remoto mediante el comando de 'mstsc' hello en PowerShell. 
3. En conexión a Escritorio remoto, escriba la dirección IP privada de Hola de hello VM. Puede haga clic en "Mostrar opciones" tooadjust adicionales configuración y luego conectarse.

### <a name="tootroubleshoot-an-rdp-connection-tooa-vm"></a>tootroubleshoot una tooa de conexión RDP VM

Si tiene problemas para conectarse a máquina virtual de tooa a través de la conexión VPN, hay algunas cosas que puede comprobar. Para obtener más información sobre solución de problemas, consulte [tooa de conexiones de escritorio remoto solucionar VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).

- Compruebe que la conexión VPN se ha establecido correctamente.
- Compruebe que se está conectando toohello dirección IP privada Hola máquina virtual.
- Use 'ipconfig' toocheck Hola dirección IPv4 asignada a toohello adaptador de Ethernet en el equipo Hola desde el que se va a conectar. Si dirección IP de hello es dentro del intervalo de direcciones de Hola de hello red virtual que se está conectando a o dentro del intervalo de direcciones de Hola de su VPNClientAddressPool, esto es tooas que se hace referencia un espacio de direcciones superpuestos. Cuando se solapa con el espacio de direcciones de esta manera, el tráfico de red hello no llegar a Azure, se mantiene en la red local de Hola.
- Si se puede conectar toohello VM con IP privada Hola de direcciones, pero no Hola nombre de equipo, compruebe que ha configurado DNS correctamente. Para más información acerca de cómo funciona la resolución de nombres para las máquinas virtuales, consulte [Resolución de nombres para las máquinas virtuales e instancias de rol](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).
- Compruebe que se generó ese paquete de configuración de cliente VPN de hello después de que se especificaron direcciones IP del servidor DNS de Hola para hello red virtual. Si ha actualizado de direcciones IP del servidor DNS de hello, generar e instalar un nuevo paquete de configuración de cliente VPN.
