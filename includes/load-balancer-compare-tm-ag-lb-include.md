## <a name="load-balancer-differences"></a>Diferencias del equilibrador de carga

No hay tráfico de red de distintas opciones toodistribute con Microsoft Azure. Estas opciones funcionan de manera diferente, ya que disponen de un conjunto de características distintas y son compatibles con escenarios distintos. Cada una se puede usar por separado, pero también se pueden combinar.

* **El equilibrador de carga Azure** funciona a la capa de transporte de hello (nivel 4 en la pila de referencia de hello OSI red). Proporciona distribución de nivel de red del tráfico entre instancias de una aplicación que se ejecuta en hello mismo centro de datos de Azure.
* **Puerta de enlace de aplicaciones** funciona a nivel de aplicación Hola (nivel 7 en la pila de referencia de hello OSI red). Actúa como un servicio de proxy inverso, finalizando la conexión de cliente de Hola y los puntos de conexión tooback-end se envían solicitudes.
* **El Administrador de tráfico** funciona en hello nivel de DNS.  Utiliza puntos de conexión DNS respuestas toodirect por el usuario final tráfico tooglobally distribuida. Los clientes, a continuación, conectarse directamente toothose extremos.

Hello en la tabla siguiente resume las características de hello ofrecidas por cada servicio:

| Servicio | Azure Load Balancer | Application Gateway | Traffic Manager |
| --- | --- | --- | --- |
| Technology |Nivel de transporte (nivel 4) |Nivel de aplicación (nivel 7) |Nivel de DNS |
| Protocolos de aplicación admitidos |Cualquiera |HTTP, HTTPS y WebSockets |Cualquiera (es necesario un punto de conexión HTTP para la supervisión del punto de conexión) |
| Extremos |Instancias de rol de máquinas virtuales de Azure y servicios en la nube |Cualquier dirección IP interna de Azure, dirección IP de Internet pública, máquina virtual de Azure, o servicio en la nube de Azure |Azure Virtual Machines, Cloud Services, Azure Web Apps y puntos de conexión externos |
| Compatibilidad de redes virtuales |Puede usarse para aplicaciones accesibles desde Internet e internas (red virtual) |Puede usarse para aplicaciones accesibles desde Internet e internas (red virtual) |Solo es compatible con aplicaciones accesibles desde Internet |
| Supervisión de puntos de conexión |Se admite a través de sondeos |Se admite a través de sondeos |Se admite a través de HTTP/HTTPS GET |

Azure equilibrador de carga y tooendpoints de tráfico de red de puerta de enlace de aplicaciones ruta pero tienen toowhich tráfico toohandle de uso distintos escenarios. Hello tabla siguiente le ayuda a comprender Hola diferenciar en los equilibradores de carga dos hello:

| Tipo | Azure Load Balancer | Application Gateway |
| --- | --- | --- |
| Protocolos |UDP/TCP |HTTP, HTTPS y WebSockets |
| Reserva de IP |Compatible |No compatible |
| Modo de equilibrio de carga |5 tuplas (IP de origen, puerto de origen, IP de destino, puerto de destino, tipo de protocolo) |Round Robin<br>Enrutamiento basado en URL |
| Modo de equilibrio de carga (IP de origen / sesiones temporales) |2 tuplas (IP de origen e IP de destino), 3 tuplas (IP de origen, IP de destino y puerto). Puede escalar hacia arriba o hacia abajo según Hola número de máquinas virtuales |Afinidad basada en cookies<br>Enrutamiento basado en URL |
| Sondeos de estado |Intervalo de sondeo predeterminado: 15 segundos. Se excluye de la rotación tras dos errores continuos. Admite sondeos definidos por el usuario |Intervalo de sondeo inactivo: 30 segundos. Se excluye tras cinco errores consecutivos de tráfico real o tras un solo error de sondeo en modo inactivo. Admite sondeos definidos por el usuario |
| Descarga de SSL |No compatible |Compatible |
| Enrutamiento basado en dirección URL | No compatible | Compatible|
| Directiva SSL | No compatible | Compatible|
