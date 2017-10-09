En este paso, probará agente de escucha del grupo de disponibilidad de Hola mediante una aplicación de cliente que se ejecuta en hello misma red.

Conectividad de cliente tiene Hola según los requisitos:

* Agente de escucha de toohello de conexiones de cliente debe proceder de equipos que residen en otro servicio de nube que Hola uno que hosts Hola réplicas de disponibilidad AlwaysOn.
* Si Hola siempre en las réplicas están en subredes diferentes, los clientes deberán especificar *MultisubnetFailover = True* en la cadena de conexión de Hola. El resultado de conexión paralelos la condición intenta tooreplicas Hola varias subredes. Este escenario incluye una implementación de grupo de disponibilidad Always On entre regiones.

Un ejemplo es el agente de escucha de tooconnect toohello desde uno de hello las máquinas virtuales en hello misma red virtual de Azure (pero no uno que hospeda una réplica). Una manera fácil toocomplete esta prueba es tootry tooconnect SQL Server Management Studio toohello agente de escucha. Otro método simple es toorun [SQLCMD.exe](https://technet.microsoft.com/library/ms162773.aspx), como se indica a continuación:

    sqlcmd -S "<ListenerName>,<EndpointPort>" -d "<DatabaseName>" -Q "select @@servername, db_name()" -l 15

> [!NOTE]
> Si es Hola valor EndpointPort *1433*, no es necesario toospecify en llamada de Hola. Hello llamada anterior también se da por supuesto que cliente hello esta toohello Unidos a un mismo dominio y que llamador hello tiene concedidos permisos de base de datos de hello mediante la autenticación de Windows.
> 
> 

Cuando se prueba el agente de escucha de hello, ser seguro toofail sobre toomake de grupo de disponibilidad de hello seguro de que los clientes pueden conectarse el agente de escucha de toohello entre conmutaciones por error.

