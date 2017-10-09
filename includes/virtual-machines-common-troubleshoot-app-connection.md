Hay varias razones cuando no se puede iniciar o conectarse tooan aplicación que se ejecuta en una máquina virtual (VM) de Azure. Razones incluyen la aplicación hello no se está ejecutando o escuchan en puertos de hello esperado, Hola escuchado puerto bloqueado o las reglas para pasar correctamente no aplicación toohello de tráfico de red. Este artículo describe un enfoque metódico toofind y un problema de hello correcto.

Si tiene problemas para conectarse tooyour VM con RDP o SSH, consulte uno de los siguientes hello en primer lugar los artículos:

* [Solucionar problemas de conexiones de escritorio remoto tooa Máquina Virtual de Azure basado en Windows](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)
* [Solucionar problemas de Shell seguro (SSH) conexiones tooa basados en Linux máquina virtual de Azure](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).

> [!NOTE]
> Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [el Administrador de recursos y el clásico](../articles/resource-manager-deployment-model.md). Este artículo incluye el uso de ambos modelos, pero Microsoft recomienda más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.

Si necesita más ayuda en cualquier momento en este artículo, puede ponerse en contacto con hello Azure expertos en [hello Azure de MSDN y Hola foros de desbordamiento de la pila](https://azure.microsoft.com/support/forums/). Como alternativa, también puede registrar un incidente de soporte técnico de Azure. Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/support/options/) y seleccione **obtener admiten**.

## <a name="quick-start-troubleshooting-steps"></a>Pasos de inicio rápido para solucionar problemas
Si tiene problemas para conectar la aplicación tooan, intente hello, siga los pasos de solución de problemas generales. Después de cada paso, intente volver a conectar aplicación de tooyour:

* Reiniciar la máquina virtual de Hola
* Vuelva a crear el extremo de Hola / las reglas de firewall / reglas de grupo (NSG) de seguridad de red
  * [Modelo de Resource Manager: administración de grupos de seguridad de red](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
  * [Modelo clásico: administración de puntos de conexión de servicios en la nube](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
* Conectarse desde otra ubicación, como una red virtual de Azure diferente
* Volver a implementar la máquina virtual de Hola
  * [Nueva implementación de la máquina virtual en Windows](../articles/virtual-machines/windows/redeploy-to-new-node.md)
  * [Nueva implementación de la máquina virtual de Linux](../articles/virtual-machines/linux/redeploy-to-new-node.md)
* Volver a crear la máquina virtual de Hola

Para obtener más información, consulte [Solución de problemas con la conectividad del punto de conexión (RDP, SSH, HTTP u otros errores)](https://social.msdn.microsoft.com/Forums/azure/en-US/538a8f18-7c1f-4d6e-b81c-70c00e25c93d/troubleshooting-endpoint-connectivity-rdpsshhttp-etc-failures?forum=WAVirtualMachinesforWindows).

## <a name="detailed-troubleshooting-overview"></a>Visión detallada de la solución de problemas
Hay cuatro áreas principales de acceso de hello tootroubleshoot de una aplicación que se ejecuta en una máquina virtual de Azure.

![solución de problemas no se puede iniciar la aplicación](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access1.png)

1. aplicación de Hola que se ejecuta en hello máquina virtual de Azure.
   * ¿Se está ejecutando correctamente propia aplicación Hola?
2. Hola máquina virtual de Azure.
   * ¿Hola propia máquina virtual ejecuta correctamente y responde toorequests?
3. Puntos de conexión de red de Azure.
   * Extremos de servicio de nube para máquinas virtuales en el modelo de implementación de hello clásico.
   * Grupos de seguridad de red y reglas NAT de entrada para las máquinas virtuales en el modelo de implementación de Resource Manager.
   * ¿Flujo de los usuarios toohello/aplicación de VM en los puertos de hello esperada del tráfico puede?
4. El dispositivo perimetral de Internet.
   * ¿Hay instauradas reglas de firewall que impidan que el tráfico fluya correctamente?

Para los equipos cliente que están accediendo a la aplicación hello a través de una conexión de sitio a sitio VPN o ExpressRoute, áreas principales de Hola que pueden causar problemas son la aplicación Hola y Hola máquina virtual de Azure.

origen de hello toodetermine de problema de Hola y su corrección, siga estos pasos.

## <a name="step-1-access-application-from-target-vm"></a>Paso 1: Acceso a la aplicación desde la máquina virtual de destino
Probar la aplicación de Hola de tooaccess con el programa de cliente apropiado de Hola de máquina virtual de hello en el que se está ejecutando. Usar el nombre de host local hello, la dirección IP local Hola o dirección de bucle invertido (127.0.0.1) de Hola.

![Inicie la aplicación directamente desde Hola VM](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access2.png)

Por ejemplo, si la aplicación hello es un servidor web, abra un explorador en hello VM e inténtelo tooaccess una página web hospedada en hello máquina virtual.

Si puede tener acceso a la aplicación hello, vaya demasiado[paso 2](#step2).

Si no se puede obtener acceso a la aplicación hello, compruebe Hola después de configuración:

* se está ejecutando la aplicación Hello en la máquina virtual de destino de Hola.
* aplicación Hello está realizando escuchas en puertos TCP y UDP de hello esperado.

En Windows y máquinas virtuales basadas en Linux, utilice hello **netstat - a** comando tooshow Hola activos puertos de escucha. Examine la salida de hello para puertos de hello esperado en el que la aplicación debe estar escuchando. Reinicie la aplicación hello o configurar puertos de hello esperada toouse según sea necesario e inténtelo de nuevo tooaccess aplicación de hello localmente.

## <a id="step2"></a>Paso 2: Obtener acceso a la aplicación desde otra máquina virtual en hello misma red virtual
Probar tooaccess Hola aplicación de una máquina virtual diferente, pero en Hola misma red virtual, con el nombre de host de la máquina virtual de Hola o su dirección IP asignada por Azure, public, private o proveedor. Para máquinas virtuales creadas con el modelo de implementación clásica de hello, no utilice la dirección IP pública de hello del servicio de nube de Hola.

![iniciar la aplicación desde una máquina virtual diferente](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access3.png)

Por ejemplo, si la aplicación hello es un servidor web, tooaccess try una página web desde un explorador en una máquina virtual diferente en Hola misma red virtual.

Si puede tener acceso a la aplicación hello, vaya demasiado[paso 3](#step3).

Si no se puede obtener acceso a la aplicación hello, compruebe Hola después de configuración:

* firewall de host de Hello en el destino de hello VM está permitiendo solicitud entrante de Hola y el tráfico de respuesta saliente.
* La detección de intrusiones o software que se ejecuta en máquinas virtuales de destino de Hola de supervisión de red está permitiendo el tráfico de Hola.
* Los puntos de conexión de servicios de nube o grupos de seguridad de red está permitiendo el tráfico de hello:
  * [Modelo clásico: administración de puntos de conexión de servicios en la nube](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
  * [Modelo de Resource Manager: administración de grupos de seguridad de red](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
* Un componente independiente que se ejecuta en la máquina virtual en la ruta de acceso de hello entre pruebas Hola VM y la máquina virtual, como un equilibrador de carga o un firewall, está permitiendo el tráfico de Hola.

En una máquina virtual basada en Windows, utilice Firewall de Windows con seguridad avanzada toodetermine si las reglas de firewall de hello excluir el tráfico entrante y saliente de la aplicación.

## <a id="step3"></a>Paso 3: Obtener acceso a la aplicación de red virtual externa de Hola
Vuelva a intentar la aplicación de hello tooaccess desde un equipo situado fuera de la red virtual de hello como VM de hello en el que se ejecuta la aplicación hello. Use una red diferente como equipo cliente de origen.

![iniciar la aplicación desde un equipo situado fuera de la red virtual de Hola](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access4.png)

Por ejemplo, si la aplicación hello es un servidor web, intente tooaccess hello web página desde un explorador que se ejecuta en un equipo que no está en la red virtual de Hola.

Si no se puede obtener acceso a la aplicación hello, compruebe Hola después de configuración:

* Para las máquinas virtuales crean utilizando el modelo de implementación clásica de hello:
  
  * Compruebe que configuración de extremo de Hola para hello que VM está permitiendo el tráfico entrante de hello, especialmente protocolo de hello (TCP o UDP) y números de puerto público y privado de Hola.
  * Compruebe que las listas de control de acceso (ACL) en el extremo de hello estén impidiendo el tráfico entrante desde Internet Hola.
  * Para obtener más información, consulte [cómo tooSet extremos tooa Máquina Virtual](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
* Para las máquinas virtuales creadas con el modelo de implementación del Administrador de recursos de hello:
  
  * Compruebe que Hola entrante configuración de la regla NAT para hello que VM está permitiendo el tráfico entrante de hello, especialmente protocolo de hello (TCP o UDP) y números de puerto público y privado de Hola.
  * Compruebe que los grupos de seguridad de red a permitir la solicitud entrante de Hola y el tráfico de respuesta saliente.
  * Para más información, consulte [¿Qué es un grupo de seguridad de red?](../articles/virtual-network/virtual-networks-nsg.md)

Si la máquina virtual de Hola o punto de conexión es un miembro de un conjunto con equilibrio de carga:

* Compruebe que el protocolo de sondeo de hello (TCP o UDP) y un número de puerto son correctos.
* Si el sondeo de hello protocolo y puerto es diferente de protocolo de conjunto de carga equilibrada de Hola y el puerto:
  * Compruebe que la aplicación hello está escuchando en número de puerto y protocolo de sondeo de hello (TCP o UDP) (usar **netstat – a** en hello el destino VM).
  * Compruebe que firewall de host de hello en destino Hola que VM está permitiendo solicitud de sondeo de entrada de Hola y tráfico de respuesta de sondeo de salida.

Si puede tener acceso a la aplicación hello, asegúrese de que está permitiendo el dispositivo perimetral de Internet:

* tráfico de solicitudes de aplicación de salida de Hello desde su toohello del equipo cliente máquina virtual de Azure.
* Hola tráfico de respuesta de la aplicación de entrada de hello máquina virtual de Azure.

## <a name="step-4-if-you-cannot-access-hello-application-use-ip-verify-toocheck-hello-settings"></a>Si no se puede obtener acceso a la aplicación hello, usar IP Compruebe toocheck Hola configuración el paso 4. 

Para más información, consulte [Información general sobre la supervisión de red de Azure](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview). 

## <a name="additional-resources"></a>Recursos adicionales
[Solucionar problemas de conexiones de escritorio remoto tooa Máquina Virtual de Azure basado en Windows](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)

[Solucionar problemas de Shell seguro (SSH) conexiones tooa basados en Linux máquina virtual de Azure](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md)

