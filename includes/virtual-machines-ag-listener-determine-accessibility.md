Es importante toorealize que hay dos tooconfigure formas un agente de escucha del grupo de disponibilidad en Azure. formas de Hello difieren en tipo hello de equilibrador de carga de Azure que se usa cuando crea el agente de escucha de Hola. Hello en la tabla siguiente describe las diferencias de hello:

| Tipo de equilibrador de carga | Implementación | Se debe utilizar si: |
| --- | --- | --- |
| **Externo** |Hello usa *dirección IP virtual pública* del servicio de nube de Hola que hospeda máquinas virtuales (VM), Hola. |Necesita agente de escucha de tooaccess Hola de red virtual de hello exterior, incluida desde Hola Internet. |
| **Interno** |Usa un *equilibrador de carga interno* con una dirección privada para el agente de escucha de Hola. |Puede tener acceso a agente de escucha de hello únicamente desde dentro de hello misma red virtual. Este acceso incluye una VPN de sitio a sitio en escenarios híbridos. |

> [!IMPORTANT]
> Para un agente de escucha que usa hello en la nube pública dirección VIP del servicio (equilibrador de carga externo), siempre y cuando el cliente de hello, el agente de escucha y las bases de datos están en Hola la misma región de Azure, no implicará cargos de salida. En caso contrario, los datos se devuelven a través de hello agente de escucha se considera la salida, y se cargan a velocidades de transferencia de datos normal. 
> 
> 

Un ILB solo se puede configurar en redes virtuales con un ámbito regional. Las redes virtuales existentes que se han configurado para un grupo de afinidad no pueden usar un ILB. Para más información, consulte [Información general sobre el equilibrador de carga interno](../articles/load-balancer/load-balancer-internal-overview.md).

