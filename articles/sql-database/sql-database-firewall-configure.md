---
title: las reglas de firewall de base de datos SQL de aaaAzure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconfigure SQL base de datos firewall con acceso de toomanage de reglas de firewall de nivel de servidor y base de datos."
keywords: firewall de base de datos
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: ac57f84c-35c3-4975-9903-241c8059011e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 04/10/2017
ms.author: rickbyh
ms.openlocfilehash: 6a8cdf629d0d0e55421a5e9f9b894a21371be568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-server-level-and-database-level-firewall-rules"></a>Reglas de firewall de nivel de servidor y de nivel de base de datos de Azure SQL Database 

Microsoft Azure SQL Database ofrece un servicio de base de datos relacional para Azure y otras aplicaciones basadas en Internet. toohelp proteger los datos, firewalls impedir que todos los servidores de base de datos de access tooyour hasta que especifique qué equipos tienen permiso. firewall de Hello otorga toodatabases de acceso basado en hello procedentes de la dirección IP de cada solicitud.

## <a name="overview"></a>Información general

Inicialmente, todos los servidor de SQL Azure de tooyour de acceso de Transact-SQL está bloqueado por firewall de Hola. toobegin con el servidor SQL Azure, debe especificar una o varias reglas de firewall de nivel de servidor que permiten el acceso a tooyour Azure SQL server. Utilice toospecify de reglas de firewall de hello dirección IP que va de hello Internet se permiten y si las aplicaciones de Azure pueden intentar tooconnect tooyour servidor SQL de Azure.

tooselectively toojust de acceso de concesión de una de las bases de datos de hello en el servidor de SQL Azure, debe crear una regla de nivel de base de datos para la base de datos necesarios de Hola. Especifique un intervalo de direcciones IP de regla de firewall de base de datos de Hola que está más allá de hello intervalo especificado en la regla de firewall de nivel de servidor de Hola de direcciones IP y asegúrese de que Hola dirección IP del Hola cliente está en intervalo de hello especificado en la regla de nivel de base de datos de Hola.

Hola de intentos de conexión desde Internet y Azure debe atravesar primero firewall Hola antes de poder alcanzar su servidor de SQL Azure o base de datos de SQL, como se muestra en hello siguiente diagrama:

   ![Diagrama donde se describe la configuración del firewall.][1]

* **Las reglas de firewall de nivel de servidor:** estas reglas permiten a los clientes tooaccess todo el servidor de SQL Azure, es decir, todas las bases de datos de Hola de Hola mismo servidor lógico. Estas reglas se almacenan en hello **maestro** base de datos. Las reglas de firewall de nivel de servidor pueden configurarse mediante el portal de Hola o mediante instrucciones Transact-SQL. reglas de firewall de nivel de servidor de toocreate con hello portal de Azure o con PowerShell, debe ser propietario de la suscripción de Hola o de un colaborador de suscripción. toocreate una regla de firewall de nivel de servidor mediante Transact-SQL, debe conectarse la instancia de base de datos SQL de toohello como inicio de sesión principal del nivel de servidor de Hola o un administrador de Azure Active Directory hello (lo que significa que primero se debe crear una regla de firewall de nivel de servidor un usuario con permisos de nivel de Azure).
* **Las reglas de firewall de nivel de base de datos:** estas reglas permiten a clientes tooaccess ciertos (seguro) bases de datos dentro de hello mismo servidor lógico. Puede crear estas reglas para cada base de datos (incluidos hello **maestro** database0) y se almacenan en bases de datos individuales de Hola. Las reglas de firewall de nivel de base de datos solo pueden configurarse mediante instrucciones Transact-SQL y solo después de haber configurado Hola primer firewall de nivel de servidor. Si especifica un intervalo de direcciones IP en la regla de firewall de nivel de base de datos de Hola que es el intervalo de hello exterior especificado en la regla de firewall de nivel de servidor de hello, solo los clientes que tengan direcciones IP en el intervalo de nivel de base de datos de hello pueden tener acceso a la base de datos de Hola. Puede tener un máximo de 128 reglas de firewall de nivel de base de datos para una base de datos. Solo se pueden crear reglas de firewall de nivel de base de datos para las bases de datos de usuario y maestras y administrarse a través de Transact-SQL. Para obtener más información acerca de cómo configurar las reglas de firewall de nivel de base de datos, vea ejemplo de Hola más adelante en este artículo y vea [sp_set_database_firewall_rule (bases de datos de SQL Azure)](https://msdn.microsoft.com/library/dn270010.aspx).

**Recomendación:** Microsoft recomienda el uso de reglas de firewall de nivel de base de datos siempre que sea posible tooenhance seguridad y toomake la base de datos más portátil. Utilizar reglas de firewall de nivel de servidor para los administradores y si tiene muchas bases de datos que han Hola mismos requisitos de acceso y no desea tiempo toospend configurar individualmente cada base de datos.

> [!Note]
> Para obtener información acerca de las bases de datos portables en contexto de Hola de continuidad del negocio, consulte [requisitos de autenticación para la recuperación ante desastres](sql-database-geo-replication-security-config.md).
>

### <a name="connecting-from-hello-internet"></a>La conexión desde Internet Hola

Cuando un equipo intenta tooconnect tooyour servidor de base de datos de Internet de hello, firewall de hello comprueba primero Hola procedentes de la dirección IP de solicitud de hello según las reglas de firewall de nivel de base de datos de hello, para base de datos de Hola que está solicitando conexión hello:

* Si es dirección IP de saludo de solicitud de hello en uno de los intervalos de hello especificados en las reglas de firewall de nivel de base de datos de hello, conexión Hola se concede toohello base de datos de SQL que contiene la regla de Hola.
* Si dirección IP de saludo de solicitud de hello no está dentro de uno de los intervalos de hello especificados en la regla de firewall de nivel de base de datos de hello, se comprueban las reglas de firewall de nivel de servidor de Hola. Si dirección IP de saludo de solicitud de hello es dentro de uno de los intervalos de hello especificados en las reglas de firewall de nivel de servidor de hello, se concede la conexión Hola. Las reglas de firewall de nivel de servidor aplican tooall bases de datos SQL en el servidor de SQL Azure Hola.  
* Si dirección IP de saludo de solicitud de hello no está dentro de intervalos de hello especifican en cualquiera de hello nivel de base de datos o reglas de firewall de nivel de servidor, se produce un error en la solicitud de conexión de Hola.

> [!NOTE]
> tooaccess base de datos de SQL Azure desde el equipo local, asegúrese de firewall de hello en la red y el equipo local permita la comunicación saliente en el puerto TCP 1433.
> 

### <a name="connecting-from-azure"></a>Conexión desde Azure
deben habilitarse tooallow aplicaciones de Azure tooconnect tooyour servidor SQL Azure, las conexiones de Azure. Cuando una aplicación de Azure intenta el servidor de base de datos de tooconnect tooyour, firewall de hello comprueba que se permiten las conexiones de Azure. Un configuración del firewall con inicial y final too0.0.0.0 igual de dirección indica que se permiten las conexiones. Si no se permite el intento de conexión de hello, solicitud de hello no alcanza servidor de base de datos de SQL Azure Hola.

> [!IMPORTANT]
> Esta opción configura Hola firewall tooallow todas las conexiones desde las conexiones incluidas Azure en suscripciones de Hola de otros clientes. Al seleccionar esta opción, asegúrese de que el inicio de sesión y permisos de usuario limitan tooonly de acceso a los usuarios autorización.
> 

## <a name="creating-and-managing-firewall-rules"></a>Creación y administración de reglas de firewall
primera configuración del firewall de nivel de servidor Hello puede crearse con hello [portal de Azure](https://portal.azure.com/) o utilizando mediante programación [Azure PowerShell](https://msdn.microsoft.com/library/azure/dn546724.aspx), [Azure CLI](/cli/azure/sql/server/firewall-rule#create), o hello [API de REST](https://msdn.microsoft.com/library/azure/dn505712.aspx). Las reglas de firewall de nivel de servidor posteriores se pueden crear y administrar mediante estos métodos, y mediante Transact-SQL. 

> [!IMPORTANT]
> Las reglas de firewall de nivel de base de datos solo pueden crearse y administrarse mediante Transact-SQL. 
>

rendimiento de tooimprove, firewall de nivel de servidor se almacenan en caché temporalmente las reglas en el nivel de base de datos de Hola. caché de hello toorefresh, consulte [DBCC FLUSHAUTHCACHE](https://msdn.microsoft.com/library/mt627793.aspx). 

> [!TIP]
> Puede usar [auditoría de base de datos de SQL](sql-database-auditing.md) tooaudit cambios en el firewall de nivel de servidor y base de datos.
>

### <a name="azure-portal"></a>Azure Portal

tooset una regla de firewall de nivel de servidor en hello portal de Azure, o bien puede ir toohello página de información general de la página de información general de Hola o de base de datos de SQL Azure del servidor lógico de la base de datos de Azure.

> [!TIP]
> Para obtener un tutorial, vea [crear una base de datos con Hola portal de Azure](sql-database-get-started-portal.md).
>

**Desde la página de información general de la base de datos**

1. tooset una regla de firewall de nivel de servidor de la página de información general de la base de datos de hello, haga clic en **Configurar firewall de servidor** en barra de herramientas de hello como se muestra en hello después de imagen: Hola **configuración del Firewall** página de hello SQL Se abre el servidor de base de datos.

      ![regla de firewall del servidor](./media/sql-database-get-started-portal/server-firewall-rule.png) 

2. Haga clic en **agregar dirección IP del cliente** en hello barra de herramientas tooadd Hola dirección IP del equipo de Hola que está usando actualmente y, a continuación, haga clic en **guardar**. Se creará una regla de firewall de nivel de servidor para la dirección IP actual.

      ![establecer regla de firewall del servidor](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

**Desde la página de información general del servidor**

página de información general para abrir el servidor, que muestra que Hola totalmente Hello calificado nombre del servidor (como **mynewserver20170403.database.windows.net**) y proporciona opciones para otra configuración.

1. tooset una regla de nivel de servidor de la página de información general del servidor, haga clic en **Firewall** en el menú izquierdo de hello en la configuración tal y como se ha explicado en hello después de la imagen: 

     ![información general del servidor lógico](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. Haga clic en **agregar dirección IP del cliente** en hello barra de herramientas tooadd Hola dirección IP del equipo de Hola que está usando actualmente y, a continuación, haga clic en **guardar**. Se creará una regla de firewall de nivel de servidor para la dirección IP actual.

     ![establecer regla de firewall del servidor](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

### <a name="transact-sql"></a>Transact-SQL
| Vista de catálogo o un procedimiento almacenado | Level | Descripción |
| --- | --- | --- |
| [sys.firewall_rules](https://msdn.microsoft.com/library/dn269980.aspx) |Server |Muestra las reglas de firewall de nivel de servidor actuales Hola |
| [sp_set_firewall_rule](https://msdn.microsoft.com/library/dn270017.aspx) |Server |Crea o actualiza las reglas de firewall de nivel de servidor |
| [sp_delete_firewall_rule](https://msdn.microsoft.com/library/dn270024.aspx) |Server |Elimina las reglas de firewall de nivel de servidor |
| [sys.database_firewall_rules](https://msdn.microsoft.com/library/dn269982.aspx) |Base de datos |Muestra las reglas de firewall de nivel de base de datos actual Hola |
| [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) |Base de datos |Crea o actualiza las reglas de firewall de nivel de base de datos de Hola |
| [sp_delete_database_firewall_rule](https://msdn.microsoft.com/library/dn270030.aspx) |Bases de datos |Elimina las reglas de firewall de nivel de base de datos |


Hello en los ejemplos siguientes revisión las reglas existentes hello, habilite un intervalo de direcciones IP en el servidor de hello Contoso y elimina una regla de firewall:
   
```sql
SELECT * FROM sys.firewall_rules ORDER BY name;
```
  
A continuación, agregue una regla de firewall.
   
```sql
EXECUTE sp_set_firewall_rule @name = N'ContosoFirewallRule',
   @start_ip_address = '192.168.1.1', @end_ip_address = '192.168.1.10'
```

toodelete una regla de firewall de nivel de servidor, Ejecutar procedimiento sp_delete_firewall_rule almacenado de Hola. Hello en el ejemplo siguiente se elimina regla Hola denominada ContosoFirewallRule:
   
```sql
EXECUTE sp_delete_firewall_rule @name = N'ContosoFirewallRule'
```   

### <a name="azure-powershell"></a>Azure PowerShell
| Cmdlet | Level | Description |
| --- | --- | --- |
| [Get-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546731.aspx) |Server |Devuelve las reglas de firewall de nivel de servidor actuales Hola |
| [New-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546724.aspx) |Server |Crear una regla de firewall de nivel de servidor |
| [Set-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546739.aspx) |Server |Actualiza las propiedades de Hola de una regla de firewall de nivel de servidor existente |
| [Remove-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546727.aspx) |Server |Elimina las reglas de firewall de nivel de servidor |


Hola de ejemplo siguiente establece una regla de firewall de nivel de servidor mediante PowerShell:

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
```

> [!TIP]
> En los ejemplos de PowerShell de contexto de Hola de un inicio rápido, consulte [crear DB - PowerShell](sql-database-get-started-powershell.md) y [crear una base de datos y configurar una regla de firewall con PowerShell](scripts/sql-database-create-and-configure-database-powershell.md)
>

### <a name="azure-cli"></a>CLI de Azure
| Cmdlet | Level | Descripción |
| --- | --- | --- |
| [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) | Crea un tooall de acceso tooallow de regla de firewall bases de datos SQL en servidor de Hola de intervalo de direcciones IP de hello especificado.|
| [az sql server firewall delete](/cli/azure/sql/server/firewall-rule#delete)| Elimina una regla de firewall.|
| [az sql server firewall list](/cli/azure/sql/server/firewall-rule#list)| Enumera las reglas de firewall de Hola.|
| [az sql server firewall rule show](/cli/azure/sql/server/firewall-rule#show)| Muestra los detalles de Hola de una regla de firewall.|
| [ax sql server firewall rule update](/cli/azure/sql/server/firewall-rule#update)| Actualiza una regla de firewall.

Hola de ejemplo siguiente establece una regla de firewall de nivel de servidor mediante Hola CLI de Azure: 

```azurecli-interactive
az sql server firewall-rule create --resource-group myResourceGroup --server $servername \
    -n AllowYourIp --start-ip-address 0.0.0.0 --end-ip-address 0.0.0.0
```

> [!TIP]
> Para obtener un ejemplo de CLI de Azure en el contexto de Hola de un inicio rápido, consulte [crear DDB - Azure CLI](sql-database-get-started-cli.md) y [crear una base de datos y configurar una regla de firewall mediante Hola CLI de Azure](scripts/sql-database-create-and-configure-database-cli.md)
>

### <a name="rest-api"></a>API de REST
| API | Level | Description |
| --- | --- | --- |
| [Enumerar reglas de firewall](https://msdn.microsoft.com/library/azure/dn505715.aspx) |Server |Muestra las reglas de firewall de nivel de servidor actuales Hola |
| [Crear regla de firewall](https://msdn.microsoft.com/library/azure/dn505712.aspx) |Server |Crea o actualiza las reglas de firewall de nivel de servidor |
| [Establecer regla de firewall](https://msdn.microsoft.com/library/azure/dn505707.aspx) |Server |Actualiza las propiedades de Hola de una regla de firewall de nivel de servidor existente |
| [Eliminar regla de firewall](https://msdn.microsoft.com/library/azure/dn505706.aspx) |Server |Elimina las reglas de firewall de nivel de servidor |

## <a name="server-level-firewall-rule-versus-a-database-level-firewall-rule"></a>Regla de firewall de nivel de servidor frente a una regla de firewall de nivel de base de datos
P: ¿Los usuarios de una base de datos deben estar completamente aislados de otra base de datos?   
  Si es así, conceda acceso usando reglas de firewall de nivel de base de datos. Esto evita el uso de reglas de firewall de nivel de servidor, que permiten el acceso a través de firewall de hello tooall bases de datos, reducir la profundidad de Hola de sus defensas.   
 
P: ¿Los usuarios en la dirección IP de hello necesita acceso a las bases de tooall?   
  Use firewall de nivel de servidor reglas tooreduce Hola número de veces que se debe configurar las reglas de firewall.   

P: ¿Persona de Hola o equipo configurar reglas de firewall de hello sólo tiene acceso a través de Hola portal de Azure, PowerShell o API de REST de Hola?   
  Debe usar reglas de firewall de nivel de servidor. Las reglas de firewall de nivel de base de datos solo pueden configurarse mediante Transact-SQL.  

P: ¿Es persona Hola o equipo configurar reglas de firewall de hello prohíbe que tengan permiso de alto nivel en el nivel de base de datos de hello?   
  Use reglas de firewall de nivel de servidor. Configuración de reglas de firewall de nivel de base de datos mediante Transact-SQL, necesita al menos `CONTROL DATABASE` permiso en el nivel de base de datos de Hola.  

P: ¿Es Hola persona o equipo configuración o auditoría de reglas de firewall de hello, administrar de forma centralizada las reglas de firewall para muchos (quizás 100) de bases de datos?   
  Esta decisión depende de sus necesidades y del entorno. Las reglas de firewall de nivel de servidor pueden ser más fácil tooconfigure, pero el scripting puede configurar reglas en hello nivel de base de datos. E incluso si usa las reglas de firewall de nivel de servidor, podría necesitar las reglas de firewall de base de datos de hello tooaudit, toosee si los usuarios con `CONTROL` permiso en la base de datos de hello haya creado las reglas de firewall de nivel de base de datos.   

P: ¿Puedo usar una combinación de reglas de firewall de nivel de servidor y de base de datos?   
  Sí. Algunos usuarios, por ejemplo, los administradores, pueden necesitar reglas de firewall de nivel de servidor. Otros usuarios, como los usuarios de una aplicación de base de datos, pueden necesitar reglas de firewall de nivel de base de datos.   

## <a name="troubleshooting-hello-database-firewall"></a>Solucionar problemas de firewall de base de datos de Hola
Considere la posibilidad de hello siguientes puntos cuando acceso toohello servicio de base de datos de SQL de Microsoft Azure no se comporta tal y como esperaba:

* **Configuración del firewall local:** antes de que el equipo puede tener acceso a la base de datos de SQL Azure, puede que necesite toocreate una excepción de firewall en el equipo para el puerto TCP 1433. Si va a realizar las conexiones dentro del límite de la nube de Azure de hello, puede tener puertos adicionales tooopen. Para obtener más información, vea hello **base de datos SQL: fuera de vs en** sección de [puertos más allá de 1433 para la base de datos de SQL y ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).
* **Traducción de direcciones (NAT) de red:** vencimiento tooNAT, dirección IP de hello usada por la tooAzure de tooconnect equipo base de datos SQL puede ser distinta de la dirección IP de Hola se muestra en las opciones de configuración de IP de equipo. dirección IP tooview Hola que el equipo está usando tooconnect tooAzure, inicie sesión en el portal de toohello y navegue toohello **configurar** ficha en servidor de Hola que hospeda la base de datos. En hello **direcciones IP permitidas** sección hello **dirección IP del cliente actual** se muestra. Haga clic en **agregar** toohello **direcciones IP permitidas** tooallow este servidor de hello tooaccess de equipo.
* **Lista de admisión de toohello de cambios no han surtido efecto todavía:** puede haber tanto como un retraso de cinco minutos para cambia el efecto de tootake de configuración de toohello base de datos de SQL Azure firewall.
* **inicio de sesión de Hello no está autorizado o se usó una contraseña incorrecta:** si un inicio de sesión no tiene permisos en el servidor de base de datos de SQL Azure de Hola o contraseña Hola utilizada es incorrecta, se deniega el servidor de base de datos de SQL Azure de hello conexión toohello. Crear una configuración de firewall sólo proporciona a los clientes un tooattempt oportunidad conectar el servidor de tooyour; cada cliente debe proporcionar credenciales de seguridad necesarias Hola. Para obtener más información sobre la preparación de inicios de sesión, vea Administración de bases de datos, inicios de sesión y usuarios en la Base de datos SQL de Azure.
* **Dirección IP dinámica:** si tiene una conexión a Internet con una dirección IP dinámica y tiene problemas para superar el firewall de hello, intente una de hello siguientes soluciones:
  
  * Pregunte a su proveedor de servicios de Internet (ISP) para el intervalo de direcciones IP de hello asignado tooyour los equipos cliente ese servidor de base de datos de SQL Azure Hola de acceso y, a continuación, agregar el intervalo de direcciones IP de hello como una regla de firewall.
  * Obtener una dirección IP estática en su lugar para los equipos cliente y, a continuación, agregue las direcciones IP hello como reglas de firewall.

## <a name="next-steps"></a>Pasos siguientes

- Para consultar un inicio rápido sobre cómo crear una base de datos y una regla de firewall de nivel de servidor, vea [Creación de una instancia de Azure SQL Database](sql-database-get-started-portal.md).
- Para obtener ayuda en la base de datos de conexión tooan SQL Azure de código abierto o aplicaciones de terceros, consulte [tooSQL base de datos de ejemplos de código de inicio rápido de cliente](https://msdn.microsoft.com/library/azure/ee336282.aspx).
- Para obtener información sobre puertos adicionales que puede necesitar tooopen, vea hello **base de datos SQL: fuera de vs en** sección de [puertos más allá de 1433 para la base de datos de SQL y ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md)
- Para obtener información general sobre la seguridad de Azure SQL Database, vea [Protección de bases de datos SQL](sql-database-security-overview.md).

<!--Image references-->
[1]: ./media/sql-database-firewall-configure/sqldb-firewall-1.png
