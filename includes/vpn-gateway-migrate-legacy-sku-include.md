> [!NOTE]
> * puerta de enlace VPN de Hello dirección IP pública cambiará al migrar desde una antigua tooa SKU SKU nuevo.
> * No se pueden migrar clásico toohello de puertas de enlace VPN SKU nuevo. VPN puertas de enlace puede solo uso clásico Hola heredadas SKU (antiguas).
> 

No se puede cambiar el tamaño de la VPN de Azure y puertas de enlace entre Hola SKU antiguas Hola nuevas familias de SKU. Si dispone de puertas de enlace VPN en el modelo de implementación del Administrador de recursos de Hola que están usando la versión anterior de Hola de hello SKU, puede migrar toohello SKU nuevo. toomigrate, que elimina la puerta de enlace VPN existente hello para la red virtual y luego cree uno nuevo.

Flujo de trabajo de la migración:

1. Quitar ninguna puerta de enlace de red virtual de toohello de conexiones.
2. Elimine la puerta de enlace VPN antiguo Hola.
3. Crear nueva la puerta de enlace VPN Hola.
4. Actualice los dispositivos VPN local con hello nueva dirección IP de VPN puerta de enlace (para conexiones de sitio a sitio).
5. Actualizar el valor de dirección IP de puerta de enlace de Hola para las puertas de enlace de red local de red virtual a red virtual que se conectará la puerta de enlace de toothis.
6. Descargar nuevos paquetes de configuración de VPN de cliente para clientes de P2S conexión toohello de red virtual a través de esta puerta de enlace VPN.
7. Vuelva a crear la puerta de enlace de red virtual de hello conexiones toohello.
