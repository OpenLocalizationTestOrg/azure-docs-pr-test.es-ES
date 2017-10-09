---
title: "aaaFix un error de conexión de SQL, error transitorio | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tootroubleshoot, diagnosticar y evitar un error de conexión de SQL o un error transitorio en la base de datos de SQL Azure. "
keywords: "conexión de sql, cadena de conexión, problemas de conectividad, error transitorio, error de conexión"
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: efb35451-3fed-4264-bf86-72b350f67d50
ms.service: sql-database
ms.custom: develop apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: d225e610b9e88170ab53ca16d615bd07220603cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a>Acciones para solucionar problemas, diagnosticar y evitar errores de conexión y errores transitorios en Base de datos SQL
Este artículo describe cómo tooprevent, solucionar problemas, diagnosticar y mitigar los errores de conexión y los errores transitorios que se encuentra la aplicación cliente cuando interactúa con la base de datos de SQL Azure. Obtenga información acerca de cómo tooconfigure lógica de reintento, generar la cadena de conexión de Hola y ajuste otros parámetros de conexión.

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a>Errores transitorios
Un error transitorio es un error que tiene una causa subyacente que pronto se solucionará automáticamente. Una causa ocasional de los errores transitorios es cuando Hola sistema Azure rápidamente desplaza hardware recursos toobetter equilibrio de carga a diversas cargas de trabajo. La mayoría de estos eventos de reconfiguración a menudo se completan en menos de 60 segundos. Durante este intervalo de tiempo de reconfiguración, tendrá conectividad emite tooAzure base de datos SQL. Aplicaciones que se conectan tooAzure debe ser la base de datos de SQL compilada tooexpect estos errores transitorios, identificador de ellos mediante la implementación de lógica en su código en lugar de ponerlos al toousers como errores de aplicación de reintento.

Si su programa cliente utiliza ADO.NET, el programa se dijo sobre error transitorio de Hola por throw Hola de un **SqlException**. Hola **número** propiedad se pueden comparar con la lista de Hola de errores transitorios en parte superior de Hola de tema de hello: [códigos de error SQL para las aplicaciones de cliente de base de datos SQL](sql-database-develop-error-messages.md).

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a>Comparación de conexión y comando
Que vuelva a intentar la conexión SQL Hola o establecer de nuevo, según la siguiente hello:

* **Se produce un error transitorio durante un intento de conexión**: se debe reintentar la conexión de hello después retrasar durante unos segundos.
* **Se produce un error transitorio durante un comando de consulta SQL**: comando hello no se debe reintentar inmediatamente. En su lugar, después de un retraso, Hola debe ser recién establecer conexión. A continuación, se puede recuperar el comando Hola.

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a>Lógica de reintento para errores transitorios.
Los programas cliente que encuentran ocasionalmente un error transitorio son más sólidos cuando contienen lógica de reintento.

Cuando el programa se comunica con la base de datos de SQL Azure a través de un middleware parte 3ª, consultar con el proveedor de hello si Hola middleware contiene lógica de reintento para errores transitorios.

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a>Principios de reintento
* Debe reintentarse una tooopen de intento de una conexión si Hola error es transitorio.
* No se debe volver a intentar directamente una instrucción SELECT de SQL que haya fallado con un error transitorio.
  
  * En su lugar, establecer una conexión nueva y, a continuación, vuelva a intentar Hola seleccione.
* Cuando una instrucción SQL UPDATE produce un error transitorio, se debe establecer una conexión nueva antes de Hola que se vuelve a intentar la actualización.
  
  * lógica de reintento de Hello debe asegurarse de que transacción de base de datos completa de hello completa o esa transacción completa Hola se revierte.

#### <a name="other-considerations-for-retry"></a>Otras consideraciones para el reintento
* Un programa por lotes que se inicia automáticamente después del horario de trabajo y que se completará antes de mañana, puede permitirse a toovery paciente con largos intervalos de tiempo entre los reintentos.
* Un programa de la interfaz de usuario debe contar con hello tendencia humana toogive seguridad después de una espera demasiado larga.
  
  * Sin embargo, solución de hello no debe ser tooretry cada pocos segundos, porque esa directiva puede saturar el sistema Hola con las solicitudes.

#### <a name="interval-increase-between-retries"></a>Aumento del intervalo entre reintentos
Se recomienda un retraso de 5 segundos antes del primer reintento. Reintentar después de un retraso inferior a 5 segundos corre el riesgo de servicio en la nube Hola abrumador. Para cada reintento subsiguientes retraso Hola debe crecer exponencialmente, tooa máximo de 60 segundos.

Obtener una explicación de hello *período de bloqueo* para los clientes que utilizan ADO.NET está disponible en [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).

Puede que le interese tooset un número máximo de reintentos antes de programa Hola finaliza automáticamente.

#### <a name="code-samples-with-retry-logic"></a>Ejemplos de código con lógica de reintento
Los ejemplos de código con lógica de reintento, en una variedad de lenguajes de programación, están disponibles en:

* [Bibliotecas de conexiones para Base de datos SQL y SQL Server](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a>Probar su lógica de reintento
tootest la lógica de reintento, se debe simular o producirá un error que puede corregirse mientras el programa se está ejecutando.

##### <a name="test-by-disconnecting-from-hello-network"></a>Probar mediante la desconexión de la red de Hola
Una manera que puede probar la lógica de reintento es toodisconnect el equipo cliente desde Hola de red mientras se ejecuta el programa Hola. error de Hello será:

* **SqlException.Number** = 11001
* Mensaje: "Host desconocido"

Como parte del programa Hola primero intente de nuevo intento, el programa puede corregir el error ortográfico hello y, a continuación, intente tooconnect.

toomake este práctico, desconecte el equipo de red de hello antes de iniciar el programa. A continuación, el programa reconoce un parámetro de tiempo de ejecución que hace que programa Hola:

1. Agregue temporalmente 11001 lista tooits de tooconsider de errores como transitorio.
2. Intente su primera conexión como de costumbre.
3. Después de Hola se captura el error, quite 11001 de lista de Hola.
4. Mostrar un mensaje que indica el equipo de hello usuario tooplug hello en red Hola.
   * Detenga la ejecución aún más mediante el uso de cualquier hello **Console.ReadLine** método o un cuadro de diálogo con un botón Aceptar. usuario de Hello presiona tecla ENTRAR de hello después de equipo de hello conectado en red de Hola.
5. Vuelva a intentar tooconnect, espera correcto.

##### <a name="test-by-misspelling-hello-database-name-when-connecting"></a>Las pruebas por nombre de base de datos de error ortográfico Hola al conectarse
El programa deliberadamente puede escribió mal el nombre de usuario de hello antes del primer intento de conexión Hola. error de Hello será:

* **SqlException.Number** = 18456
* Mensaje: "Error de inicio de sesión para el usuario 'WRONG_MyUserName'".

Como parte del programa Hola primero intente de nuevo intento, el programa puede corregir el error ortográfico hello y, a continuación, intente tooconnect.

toomake este práctico, su programa pudo reconocer un parámetro de tiempo de ejecución que hace que programa Hola:

1. Agregue temporalmente 18456 lista tooits de tooconsider de errores como transitorio.
2. Deliberadamente Agregar nombre de usuario de toohello 'WRONG_'.
3. Después de Hola se captura el error, quite 18456 de lista de Hola.
4. Quite 'WRONG_' nombre de usuario de Hola.
5. Vuelva a intentar tooconnect, espera correcto.

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a>Parámetros .NET SqlConnection para reintento de conexión
Si su programa cliente conecta tootooAzure base de datos SQL mediante la clase de .NET Framework de hello **System.Data.SqlClient.SqlConnection**, debe utilizar .NET 4.6.1 o posterior (o .NET Core) lo que permite aprovechar su característica de reintento de conexión. Detalles de la característica de hello [aquí](http://go.microsoft.com/fwlink/?linkid=393996).

<!--
2015-11-30, FwLink 393996 points toodn632678.aspx, which links tooa downloadable .docx related tooSqlClient and SQL Server 2014.
-->


Al compilar hello [cadena de conexión](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) para su **SqlConnection** de objeto, se deben coordinar valores de hello entre Hola parámetros siguientes:

* ConnectRetryCount &nbsp;&nbsp;*(El valor predeterminado es 1. El intervalo es de 0 a 255).*
* ConnectRetryInterval &nbsp;&nbsp;*(El valor predeterminado es 1 segundo. El intervalo es de 1 a 60.)*
* Connection Timeout &nbsp;&nbsp;*(El valor predeterminado es 15 segundos. El intervalo es de 0 a 2147483647)*

En concreto, los valores elegidos deben hacer Hola después de igualdad true:

* Connection Timeout = ConnectRetryCount * ConnectionRetryInterval

Por ejemplo, si hello contar = 3 y el intervalo = 10 segundos, un tiempo de espera de solo 29 segundos no bastante proporcionaría sistema Hola tiempo suficiente para su reintento 3er y final al conectar: 29 < 3 * 10.

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a>Comparación de conexión y comando
Hola **ConnectRetryCount** y **ConnectRetryInterval** parámetros permiten la **SqlConnection** Hola de objeto vuelva a intentar la operación de conexión sin que se lo indica o molestarle su programa, como devolver el programa de tooyour de control. reintentos de Hello pueden producirse en hello siguientes situaciones:

* Llamada del método mySqlConnection.Open
* Llamada del método mySqlConnection.Execute

Hay algo muy sutil que tener en cuenta. Si se produce un error transitorio mientras su *consulta* se está ejecutando, el **SqlConnection** no Hola de reintentar la operación de conexión y por supuesto, no vuelva a intentar la consulta de objeto. Sin embargo, **SqlConnection** muy rápidamente comprobaciones Hola conexión antes de enviar la consulta para su ejecución. Si la comprobación rápida de hello detecta un problema de conexión, **SqlConnection** Hola de reintentos de la operación de conexión. Si se realiza correctamente el reintento de hello, consultar se envía para su ejecución.

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a>¿Se debe combinar Connectretrycount con lógica de reintento de la aplicación?
Supongamos que su aplicación tiene una lógica de reintento personalizada. Podría Reintentar Hola 4 veces la operación de conexión. Si agrega **ConnectRetryInterval** y **ConnectRetryCount** = 3 cadena de conexión de tooyour, aumentará la too4 de recuento de reintentos de Hola * 3 = 12 vuelve a intentar. Es posible que no desee un gran número de reintentos.

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-tooazure-sql-database"></a>Las conexiones tooAzure base de datos SQL
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a>Conexión: cadena de conexión
cadena de conexión de Hello necesaria para conectar tooAzure base de datos SQL es ligeramente diferente de cadena de Hola para conectar tooMicrosoft SQL Server. Puede copiar la cadena de conexión de hello para la base de datos de Hola [portal de Azure](https://portal.azure.com/).

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a>Conexión: Dirección IP
Debe configurar Hola base de datos SQL tooaccept comunicación entre el servidor de la dirección IP de hello del equipo de Hola que aloja su programa cliente. Para ello, editar la configuración de firewall de Hola a través de hello [portal de Azure](https://portal.azure.com/).

Si ha olvidado la dirección IP de tooconfigure hello, se producirá un error en el programa con un mensaje de error práctica que indica la dirección IP necesario Hola.

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

Para obtener más información, consulte [Configuración del firewall en Base de datos SQL](sql-database-configure-firewall-settings.md)

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a>Conexión: puertos
Normalmente sólo necesitará tooensure que el puerto 1433 está abierto para la comunicación saliente, en equipo Hola que hospeda programa cliente.

Por ejemplo, cuando el programa de cliente está alojado en un equipo Windows, Hola Firewall de Windows en el host de hello permite tooopen el puerto 1433:

1. Abra el Panel de Control de Hola
2. &gt; Todos los elementos del Panel de control
3. &gt; Firewall de Windows
4. &gt; Configuración avanzada
5. &gt; Reglas de salida
6. &gt; Acciones
7. &gt; Nueva regla

Si el programa cliente se hospeda en una máquina virtual (VM) de Azure, debe leer:<br/>[Puertos más allá del 1433 para ADO.NET 4.5 y SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).

Para obtener información general acerca de la configuración de puertos y la dirección IP, consulte: [Firewall de Base de datos SQL de Azure](sql-database-firewall-configure.md)

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a>Conexión: ADO.NET 4.6.1
Si el programa utiliza las clases de ADO.NET como **System.Data.SqlClient.SqlConnection** tooconnect tooAzure base de datos SQL, se recomienda que use .NET Framework versión 4.6.1 o superior.

ADO.NET 4.6.1:

* Base de datos de SQL Azure, hay mayor confiabilidad cuando se abre una conexión mediante el uso de hello **SqlConnection.Open** método. Hola **abiertos** método incorpora ahora mejor mecanismos de reintento de esfuerzo en errores de respuesta tootransient, para determinados errores en tiempo de espera de conexión de Hola.
* Admite la agrupación de conexiones. Esto incluye una comprobación eficaz que Hola conexión objeto proporciona el programa está funcionando.

Cuando se utiliza un objeto de conexión desde un grupo de conexiones, se recomienda que el programa temporalmente cerrar conexión hello cuando lo use no inmediatamente. Volver a abrir una conexión no es caro Hola crear una nueva conexión de forma.

Si está usando ADO.NET 4.0 o versiones anteriores, se recomienda que actualice toohello ADO.NET más reciente.

* Desde noviembre de 2015 se puede [descargar ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a>Diagnóstico
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a>Diagnóstico: Probar si las utilidades pueden conectarse
Si el programa presenta tooconnect tooAzure base de datos SQL, una opción de diagnóstico es tootry tooconnect con un programa de utilidad. Lo ideal es que se conectará la utilidad de hello mediante el uso de Hola la misma biblioteca que usa el programa.

En cualquier equipo con Windows, puede probar estas utilidades:

* SQL Server Management Studio (ssms.exe), que se conecta mediante ADO.NET.
* sqlcmd.exe, que se conecta mediante [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).

Una vez conectado, compruebe que funciona una breve consulta SELECT de SQL.

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-hello-open-ports"></a>Diagnóstico: Puertos abiertos de Hola de comprobación
Supongamos que se sospecha que se producen errores en los intentos de conexión debido a problemas de tooport. En el equipo puede ejecutar una utilidad que informa sobre las configuraciones de puerto de Hola.

En Linux Hola utilidades siguientes pueden ser útiles:

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * (Cambiar toobe de valor de ejemplo de Hola su dirección IP).

En Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utilidad puede resultar útil. Esta es una ejecución de ejemplo que consultar la situación de puerto de hello en un servidor de base de datos de SQL Azure, y que se ejecute en un equipo portátil:

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting tooresolve name tooIP address...
Name resolved too23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a>Diagnóstico: Registrar los errores
A veces un problema intermitente se diagnostica mejor mediante la detección de un patrón general durante varios días o semanas.

El cliente puede ayudar al diagnóstico mediante el registro de todos los errores que encuentra. Es posible que pueda toocorrelate entradas del registro de hello con datos de error que inicie una base de datos de SQL Azure propio internamente.

Enterprise Library 6 (EntLib60) ofrece tooassist de clases administradas de .NET con el registro:

* [5 - como fácil como están fuera de un registro de: utilizando Hola bloque de aplicación de registro](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a>Diagnóstico: Examinar los registros del sistema en busca de errores
Presentamos algunas instrucciones SELECT de Transact-SQL que consultan los registros de error y otra información.

| Consulta de un registro | Descripción |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |Hola [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) vista proporciona información acerca de los eventos individuales, incluidas algunas que pueden causar errores transitorios o errores de conectividad.<br/><br/>Lo ideal es que se puede poner en correlación hello **start_time** o **end_time** valores con información acerca de si su programa cliente tenido problemas.<br/><br/>**Sugerencia:** debe conectarse toohello **principal** la base de datos toorun esto. |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |Hola [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) Vista ofrece recuentos agregados de los tipos de eventos para realizar diagnósticos adicionales.<br/><br/>**Sugerencia:** debe conectarse toohello **principal** la base de datos toorun esto. |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-hello-sql-database-log"></a>Diagnóstico: Búsqueda para los eventos de problema de registro de base de datos SQL de Hola
Puede buscar entradas sobre los eventos del problema en el registro de hello de base de datos de SQL Azure. Intente Hola después de la instrucción SELECT de Transact-SQL en hello **maestro** base de datos:

```
SELECT
   object_name
  ,CAST(f.event_data as XML).value
      ('(/event/@timestamp)[1]', 'datetime2')                      AS [timestamp]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="error"]/value)[1]', 'int')             AS [error]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="state"]/value)[1]', 'int')             AS [state]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="is_success"]/value)[1]', 'bit')        AS [is_success]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="database_name"]/value)[1]', 'sysname') AS [database_name]
FROM
  sys.fn_xe_telemetry_blob_target_read_file('el', null, null, null) AS f
WHERE
  object_name != 'login_event'  -- Login events are numerous.
  and
  '2015-06-21' < CAST(f.event_data as XML).value
        ('(/event/@timestamp)[1]', 'datetime2')
ORDER BY
  [timestamp] DESC
;
```


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a>Algunas filas devueltas de sys.fn_xe_telemetry_blob_target_read_file
Después se muestra el aspecto de una fila devuelta. Hola valores null que se muestra a menudo no son nulos, en otras filas.

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a>Enterprise Library 6
Enterprise Library 6 (EntLib60) es un marco de clases de .NET que ayuda a implementar a los clientes sólidos de servicios en la nube, uno de los cuales es el servicio de base de datos de SQL Azure de Hola. Puede encontrar el área de temas tooeach dedicado en el que puede ayudar EntLib60 visitando primera:

* [Enterprise Library 6: abril de 2013](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

La lógica de reintento para controlar los errores transitorios es un área en la que puede ayudar EntLib60:

* [4 - su perseverancia, secreto de todos los logros: mediante Hola Transient Fault Handling Application Block](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> Hello código fuente de EntLib60 está disponible para el público [descargar](http://go.microsoft.com/fwlink/p/?LinkID=290898). Microsoft no tiene ninguna característica adicional de planes toomake tooEntLib las actualizaciones de mantenimiento o actualizaciones.
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a>Clases de EntLib60 para errores transitorios y reintentos
Hola después de las clases de EntLib60 es especialmente útil para la lógica de reintento. Hola a todos estos son en, o son más bajo, espacio de nombres **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:

*En el espacio de nombres de hello **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*

* **RetryPolicy**
  
  * **ExecuteAction**
* **ExponentialBackoff**
* **SqlDatabaseTransientErrorDetectionStrategy**
* **ReliableSqlConnection**
  
  * **ExecuteCommand**

En el espacio de nombres de hello **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:

* **AlwaysTransientErrorDetectionStrategy**
* **NeverTransientErrorDetectionStrategy**

Estos son vínculos tooinformation sobre EntLib60:

* Libre [Descargar libreta: tooMicrosoft de guía del desarrollador Enterprise Library, 2ª edición](http://www.microsoft.com/download/details.aspx?id=41145)
* Procedimientos recomendados: [Orientación general sobre reintentos](../best-practices-retry-general.md) tiene una excelente explicación detallada de la lógica de reintento.
* Descarga de NuGet de [Enterprise Library: Bloque de aplicación de control de errores transitorios 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-hello-logging-block"></a>EntLib60: bloque de registro hello
* bloque de registro de Hello es una solución altamente configurable y flexible que le permite:
  
  * Crear y almacenar los mensajes de registro en una amplia variedad de ubicaciones.
  * Clasificar y filtrar los mensajes.
  * Recopilar la información contextual es útil para la depuración y el seguimiento, así como para los requisitos de registro generales y de auditoría.
* bloque de registro de Hello abstrae Hola la funcionalidad del registro de destino de registro de hello para que el código de la aplicación hello es coherente, independientemente de la ubicación de Hola y el tipo de almacén de registro de destino de Hola.

Para obtener más información, consulte: [5 - como fácil como están fuera de un registro de: utilizando Hola bloque de aplicación de registro](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a>Código fuente del método IsTransient de EntLib60
Después, desde hello **SqlDatabaseTransientErrorDetectionStrategy** de clases, se muestra código fuente hello C# hello **IsTransient** método. código fuente de Hello aclara qué errores se tuvieron en cuenta toobe transitorio y que vuelva a intentar a partir de abril de 2013.

Numerosos **//comment** líneas se han quitado de esta legibilidad tooemphasize de copia.

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in hello exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // hello service is currently busy. Retry hello request after 10 seconds.
            // Code: (reason code toobe decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode hello reason code from hello error message to
            // determine hello grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach hello decoded values as additional attributes to
            // hello original SQL exception.
            sqlException.Data[condition.ThrottlingMode.GetType().Name] =
              condition.ThrottlingMode.ToString();
            sqlException.Data[condition.GetType().Name] = condition;

            return true;

          case 10928:
          case 10929:
          case 10053:
          case 10054:
          case 10060:
          case 40197:
          case 40540:
          case 40613:
          case 40143:
          case 233:
          case 64:
            // DBNETLIB Error Code: 20
            // hello instance of SQL Server you attempted tooconnect to
            // does not support encryption.
          case (int)ProcessNetLibErrorCode.EncryptionNotSupported:
            return true;
        }
      }
    }
    else if (ex is TimeoutException)
    {
      return true;
    }
    else
    {
      EntityException entityException;
      if ((entityException = ex as EntityException) != null)
      {
        return this.IsTransient(entityException.InnerException);
      }
    }
  }

  return false;
}
```


## <a name="next-steps"></a>Pasos siguientes
* Para solucionar otros problemas comunes de conexión de base de datos de SQL Azure, visite [tooAzure base de datos SQL de problemas de conexión de la solución de problemas](sql-database-troubleshoot-common-connection-issues.md).
* [Agrupación de conexiones de SQL Server (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [*Volver a intentar* es una licencia de Apache 2.0 general Reintentando la biblioteca, escrita en **Python**, tarea de hello toosimplify de agregar toojust de comportamiento de reintento sobre cualquier elemento.](https://pypi.python.org/pypi/retrying)

